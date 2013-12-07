---
layout: post
status: publish
published: true
title: VST 2.4 with Cygwin+MinGW32
author: Hans
author_login: fugalh
author_email: hans@fugal.net
author_url: http://hans.fugal.net/
excerpt: |-
  <p>I have been negligent in the Haas effect plugin that <a href="http://www.dilvie.com/">dilvie</a> commissioned from me (ok, he didn't exactly commision it, it was more like a vague promise to make me almost famous). I got the thing working (mostly) but delivery fell flat on its face when my first attempt at compiling it on Windows with Visual Studio 6 apparently failed.</p>

  <p>Well now that I have VMware I ran out of excuses to figure it out. I spent a couple hours trying to figure it out today and learned more than I wanted to know about DLLs, Cygwin, MinGW32, Visual Studio products, and VST.</p>
wordpress_id: 687
wordpress_url: urn:uuid:e7734ab5-9b03-4519-961e-4e4243a2df21
date: '2006-07-29 20:36:00.000000000 -07:00'
tags:
- audio
- vst
- mingw32
- cygwin
- dll
- windows
comments: []
---
<p>I have been negligent in the Haas effect plugin that <a href="http://www.dilvie.com/">dilvie</a> commissioned from me (ok, he didn't exactly commision it, it was more like a vague promise to make me almost famous). I got the thing working (mostly) but delivery fell flat on its face when my first attempt at compiling it on Windows with Visual Studio 6 apparently failed.</p>

<p>Well now that I have VMware I ran out of excuses to figure it out. I spent a couple hours trying to figure it out today and learned more than I wanted to know about DLLs, Cygwin, MinGW32, Visual Studio products, and VST.</p><a id="more"></a><a id="more-687"></a><p>A VST plugin is a DLL. I've learned that "DLL hell" refers not only to the user's point of view but the developer's as well. </p>

<p>I learned that Microsoft offers a limited "Visual C++ Express" that you can use to compile VSTs, but it involves tedious tweaking of a Visual C++ "solution". Even the solutions (project files) that come in the VST SDK don't work without tweaking on their own examples. No fun. Rather than doing that I decided to take the more intelligent (if longer) road and figure out how to do it with gcc.</p>

<p>I stumbled across <a href="http://codeblocks.org/">Code::Blocks Studio</a> which you can download bundled with MinGW (and thus skip the nightmare that is the <a href="http://mingw.org/download.shtml">MinGW download page</a>), and which also can use your Microsoft compiler. I gave it a try for awhile, and although I was impressed I wasn't able to get it to make a VST DLL without major tweaks, and since IDE tweaking is not my thing I decided to fall back on vim+make in Cygwin. </p>

<p>By this time I had gleaned enough from Google to know two things: people have had success compiling VST plugins with mingw32 and they were terrible at explaining it. I hope to do a bit better. Let the explanation begin!</p>

<p>If you haven't already, then install Cygwin and be sure to select the various development packages, including gcc, anything that says mingw, and make.</p>

<p>First off, we need a project. I copied the files from the again sample source directory (<code>again.cpp</code> and <code>again.h</code>) into my fresh new <code>again</code> directory. Then with the help of various web sites I composed the following <code>Makefile</code>:</p>

<pre>
# Substitute your values here
VST=../vstsdk2.4
PLUGIN=again
#

CXXFLAGS=-I$(VST) -I$(VST)/public.sdk/source/vst2.x -DBUILDING_DLL -mno-cygwin
LDFLAGS=
DLLWRAP=dllwrap --target=i386-mingw32 -mno-cygwin
DLL=$(PLUGIN).dll

$(DLL): $(PLUGIN).o audioeffect.o audioeffectx.o vstplugmain.o
        $(DLLWRAP) --driver-name c++ --def $(PLUGIN).def $^ -o $@

audioeffect.o: $(VST)/public.sdk/source/vst2.x/audioeffect.cpp
        $(CXX) $(CXXFLAGS) -c $<

audioeffectx.o: $(VST)/public.sdk/source/vst2.x/audioeffectx.cpp
        $(CXX) $(CXXFLAGS) -c $<

vstplugmain.o: $(VST)/public.sdk/source/vst2.x/vstplugmain.cpp
        $(CXX) $(CXXFLAGS) -c $<

clean:
        rm -f *.o $(DLL) lib$(PLUGIN).*

.PHONY: clean
</pre>

<p>If you dissect and study the makefile you will see that we are compiling things to object files then using the <code>dllwrap</code> tool to create the DLL. The magic flags are <code>-mno-cygwin</code> which tells cygwin's gcc to use the mingw headers and libraries, and the <code>--target=i386-mingw32</code> flag to <code>dllwrap</code> which does the same for <code>dllwrap</code>. You also have to make a .def file for the plugin, which seems to be the case for Visual Studio as well so you will find plenty of info about it online, but here's mine:</p>

<pre>
LIBRARY     again
DESCRIPTION 'Sample VST plugin'
EXPORTS     main=VSTPluginMain
</pre>

<p>Now if you try to compile that, it will give you warnings about failed <code>#pragma</code> statements. I have a patch to the VST 2.4 SDK to fix that:</p>

<pre>
diff -ur vstsdk2.4.orig/pluginterfaces/vst2.x/aeffect.h vstsdk2.4/pluginterfaces/vst2.x/aeffect.h
--- vstsdk2.4.orig/pluginterfaces/vst2.x/aeffect.h      2006-02-13 14:11:16.000000000 -0800
+++ vstsdk2.4/pluginterfaces/vst2.x/aeffect.h   2006-07-29 17:19:02.957125000 -0800
@@ -34,6 +34,9 @@
 #endif
 #if defined __BORLANDC__
        #pragma -a8
+#elif defined(__GNUC__) && defined(WIN32)
+       #pragma pack(push,8)
+       #define VSTCALLBACK __cdecl
 #elif defined(WIN32) || defined(__FLAT__) || defined CBUILDER
        #pragma pack(push)
        #pragma pack(8)
diff -ur vstsdk2.4.orig/pluginterfaces/vst2.x/aeffectx.h vstsdk2.4/pluginterfaces/vst2.x/aeffectx.h
--- vstsdk2.4.orig/pluginterfaces/vst2.x/aeffectx.h     2006-02-13 14:11:16.000000000 -0800
+++ vstsdk2.4/pluginterfaces/vst2.x/aeffectx.h  2006-07-29 17:19:43.910250000 -0800
@@ -26,6 +26,8 @@
        #endif
 #elif defined __BORLANDC__
        #pragma -a8
+#elif defined(__GNUC__) && defined(WIN32)
+       #pragma pack(push,8)
 #elif defined(WIN32) || defined(__FLAT__)
        #pragma pack(push)
        #pragma pack(8)
 </pre>

<p>Apply it with <code>patch -p1 &lt; vstsdk2.4.patch</code> in your <code>vstsdk2.4</code> subdirectory and you're good to go (don't worry, it won't break anything with Visual Studio).</p>

<p>I was able to compile the again plugin and it seems to be working. Now I'll just get everything else for my plugin figured out and deliver it to master dilvie.</p>
