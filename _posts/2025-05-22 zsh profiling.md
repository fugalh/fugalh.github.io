---
title: Speeding up Zsh startup
tags:
- shell
---
In a fit of procrastination I recently set up [Oh My Zsh](https://ohmyz.sh/) (OMZ) with a few themes in rotation. I'm not doing anything fantastical, the only plugin I load is the git one, and I use a pretty basic theme.

Startup on the remote linux box is about 320ms. I'd love <100ms but I can live with it. Similarly on my personal laptop it spins up in around half a second.

But on my work laptop it was frequently taking 1-2+ seconds. That's an eternity and it was driving me up the wall. It's a Mac like my personal laptop, but beefier (and they're both Apple Silicon). I was sourcing the same stuff, except a few extra things for work (turning that off was one of the first things I tried when profiling). I Googled and fiddled and even hacked OMZ internals some, but nothing was helping. It was fine if I didn't source OMZ, and slow if I did.

Long story short, it turned out to be that on my work laptop I had an ancient snippet in `~/.zlogin` that was sourcing RVM stuff. I don't use RVM and I don't remember ever using RVM but maybe at one point when I did more Ruby I was (or a dependency installed it once). I also didn't know `~/.zlogin` even existed, and I didn't know RVM had put something there. When I took it out, zsh initialization sped up to match the other boxes.

But why? My theory is that OMZ has a lot of functions, and when `compinit` takes awhile to recompile the completions database. This is *supposed* to only happen every once in awhile, when the sources change. I saw [in the manpage](https://zsh.sourceforge.io/Doc/Release/Completion-System.html#Use-of-compinit), and some articles on the web, and in the OMZ code that `compinit` ideally only runs once in `~/.zshrc` and it should be after `fpath` has stabilized. I suspect that the RVM scripts being sourced from `~/.zlogin` were changing `fpath` and running `compinit` again. The next time zsh started, it would be in a dirty state and `compinit` would recompile, and then RVM would change `fpath` and `compinit` would have to recompile again, and around we go recompiling the entirety of OMZ twice every time I make a new iTerm tab.

There's lots out there about profiling e.g. using `zprof`, and they were all somewhat helpful but the thing that helped me get to the bottom of this specific weirdness was
```zsh
time zsh --sourcetrace -lic 'echo foo'
```
That's where I saw `.rvm/` files getting sourced and traced it back to `.zlogin`. Would I have thought to look at `.zlogin` if I had [RTFM](https://zsh.sourceforge.io/Doc/Release/Files.html#Files)? Yes, but where's the fun in that?


In particular, doing `zprof` in `~/.zshrc` was completely missing the cost of `~/.zlogin` because that gets sourced after. And technically something expensive could have been in `~/.zprofile` before `~/.zshrc` started profiling. So now if a certain environment variable is set I start profiling in `~/.zprofile` and finish in `~/.zlogin`:
```zsh
# .zprofile (at the start)
# Profile zsh startup with this command:
#   time ZSH_PROFILE_STARTUP=yup zsh --sourcetrace -lic 'echo foo'
[[ -v ZSH_PROFILE_STARTUP ]] && zmodload zsh/zprof


# .zlogin (at the end)
[[ -v ZSH_PROFILE_STARTUP ]] && zprof
```
Which now looks something like this for me:
```
::= 9:49:31 ≠
λ fugalh-mbp fugalh ~/blog • time ZSH_PROFILE_STARTUP=yup zsh --sourcetrace -lic true
+/Users/fugalh/.zshenv:1> <sourcetrace>
+/etc/zprofile:1> <sourcetrace>
+/Users/fugalh/.zprofile:1> <sourcetrace>
+/etc/zshrc:1> <sourcetrace>
+/Users/fugalh/.zshrc:1> <sourcetrace>
+/Users/fugalh/etc/work/zshrc:1> <sourcetrace>
+/Users/fugalh/etc/local/zshrc:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/oh-my-zsh.sh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/tools/check_for_upgrade.sh:1> <sourcetrace>
+/Users/fugalh/.zcompdump-Maeve-5.9:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/async_prompt.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/bzr.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/cli.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/clipboard.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/compfix.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/completion.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/correction.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/diagnostics.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/directories.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/functions.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/git.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/grep.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/cache/grep-alias:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/history.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/key-bindings.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/misc.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/nvm.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/prompt_info_functions.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/spectrum.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/termsupport.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/theme-and-appearance.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/lib/vcs_info.zsh:1> <sourcetrace>
+/Users/fugalh/.oh-my-zsh/plugins/git/git.plugin.zsh:1> <sourcetrace>
+/Users/fugalh/.config/oh-my-zsh/custom/themes/fugl.zsh-theme:1> <sourcetrace>
+/Users/fugalh/.aliases:1> <sourcetrace>
+/Users/fugalh/.aliases.macos:1> <sourcetrace>
+/Users/fugalh/etc/work/aliases:1> <sourcetrace>
+/Users/fugalh/etc/local/local:1> <sourcetrace>
+/Users/fugalh/.zlogin:1> <sourcetrace>
num  calls                time                       self            name
-----------------------------------------------------------------------------------
 1)   22         148.39     6.74   82.32%    124.67     5.67   69.16%  _omz_source
 2)    1          19.32    19.32   10.72%     19.32    19.32   10.72%  test-ls-args
 3)    2          14.16     7.08    7.85%     14.16     7.08    7.85%  compaudit
 4)    1           9.65     9.65    5.35%      9.65     9.65    5.35%  zrecompile
 5)    1          21.39    21.39   11.86%      7.23     7.23    4.01%  compinit
 6)    1           2.10     2.10    1.16%      2.10     2.10    1.16%  regexp-replace
 7)    1           0.71     0.71    0.39%      0.71     0.71    0.39%  colors
 8)    6           0.65     0.11    0.36%      0.65     0.11    0.36%  is-at-least
 9)    6           0.61     0.10    0.34%      0.61     0.10    0.34%  add-zsh-hook
10)    2           0.54     0.27    0.30%      0.54     0.27    0.30%  bashcompinit
11)   13           0.48     0.04    0.26%      0.48     0.04    0.26%  compdef
12)    1           0.09     0.09    0.05%      0.05     0.05    0.03%  complete
13)    2           0.04     0.02    0.02%      0.04     0.02    0.02%  is_theme
14)    2           0.04     0.02    0.02%      0.04     0.02    0.02%  is_plugin
15)    2           0.02     0.01    0.01%      0.02     0.01    0.01%  env_default

-----------------------------------------------------------------------------------

 1)   22         148.39     6.74   82.32%    124.67     5.67   69.16%  _omz_source
       1/2         0.01     0.01    0.01%      0.01     0.01             bashcompinit [10]
       2/2         0.02     0.01    0.01%      0.02     0.01             env_default [15]
      12/13        0.44     0.04    0.24%      0.44     0.04             compdef [11]
       4/6         0.49     0.12    0.27%      0.49     0.12             add-zsh-hook [9]
       6/6         0.65     0.11    0.36%      0.65     0.11             is-at-least [8]
       1/1         0.71     0.71    0.39%      0.71     0.71             colors [7]
       1/1         2.10     2.10    1.16%      2.10     2.10             regexp-replace [6]
       1/1        19.32    19.32   10.72%     19.32    19.32             test-ls-args [2]

-----------------------------------------------------------------------------------

 5)    1          21.39    21.39   11.86%      7.23     7.23    4.01%  compinit
       1/2        14.16    14.16    7.85%      0.44     0.44             compaudit [3]

-----------------------------------------------------------------------------------

       1/1        19.32    19.32   10.72%     19.32    19.32             _omz_source [1]
 2)    1          19.32    19.32   10.72%     19.32    19.32   10.72%  test-ls-args

-----------------------------------------------------------------------------------

       1/2        14.16    14.16    7.85%      0.44     0.44             compinit [5]
       1/2        13.72    13.72    7.61%     13.72    13.72             compaudit [3]
 3)    2          14.16     7.08    7.85%     14.16     7.08    7.85%  compaudit
       1/2        13.72    13.72    7.61%     13.72    13.72             compaudit [3]

-----------------------------------------------------------------------------------

 4)    1           9.65     9.65    5.35%      9.65     9.65    5.35%  zrecompile

-----------------------------------------------------------------------------------

       1/1         2.10     2.10    1.16%      2.10     2.10             _omz_source [1]
 6)    1           2.10     2.10    1.16%      2.10     2.10    1.16%  regexp-replace

-----------------------------------------------------------------------------------

       1/1         0.71     0.71    0.39%      0.71     0.71             _omz_source [1]
 7)    1           0.71     0.71    0.39%      0.71     0.71    0.39%  colors

-----------------------------------------------------------------------------------

       6/6         0.65     0.11    0.36%      0.65     0.11             _omz_source [1]
 8)    6           0.65     0.11    0.36%      0.65     0.11    0.36%  is-at-least

-----------------------------------------------------------------------------------

       4/6         0.49     0.12    0.27%      0.49     0.12             _omz_source [1]
 9)    6           0.61     0.10    0.34%      0.61     0.10    0.34%  add-zsh-hook

-----------------------------------------------------------------------------------

       1/2         0.01     0.01    0.01%      0.01     0.01             _omz_source [1]
10)    2           0.54     0.27    0.30%      0.54     0.27    0.30%  bashcompinit

-----------------------------------------------------------------------------------

      12/13        0.44     0.04    0.24%      0.44     0.04             _omz_source [1]
       1/13        0.04     0.04    0.02%      0.04     0.04             complete [12]
11)   13           0.48     0.04    0.26%      0.48     0.04    0.26%  compdef

-----------------------------------------------------------------------------------

12)    1           0.09     0.09    0.05%      0.05     0.05    0.03%  complete
       1/13        0.04     0.04    0.02%      0.04     0.04             compdef [11]

-----------------------------------------------------------------------------------

13)    2           0.04     0.02    0.02%      0.04     0.02    0.02%  is_theme

-----------------------------------------------------------------------------------

14)    2           0.04     0.02    0.02%      0.04     0.02    0.02%  is_plugin

-----------------------------------------------------------------------------------

       2/2         0.02     0.01    0.01%      0.02     0.01             _omz_source [1]
15)    2           0.02     0.01    0.01%      0.02     0.01    0.01%  env_default
+/Users/fugalh/.zlogout:1> <sourcetrace>
ZSH_PROFILE_STARTUP=yup zsh --sourcetrace -lic true  0.15s user 0.16s system 53% cpu 0.574 total
```
