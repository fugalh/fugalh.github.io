---
title: DV Mezzanine transcode for DaVinci Resolve with HandBrake
tags:
- video
---
I've been using [DaVinci Resolve](https://www.blackmagicdesign.com/products/davinciresolve) for video editing lately, and I'm liking it a lot.

I've been organizing old hard drives and found some old camcorder footage in the form of `.dv` files. 

```
ffprobe version 7.1 Copyright (c) 2007-2024 the FFmpeg developers
...
Input #0, dv, from '/Volumes/Tick/Footage/Camcorder.iMovieProject/Media/Clip 35.dv':
  Duration: 00:00:22.22, start: 0.000000, bitrate: 28771 kb/s
  Stream #0:0: Video: dvvideo, yuv411p, 720x480 [SAR 32:27 DAR 16:9], 28771 kb/s, 60k fps, 29.97 tbr, 60k tbn
  Stream #0:1: Audio: pcm_s16le, 32000 Hz, stereo, s16, 1024 kb/s
  Stream #0:2: Audio: pcm_s16le, 32000 Hz, stereo, s16, 1024 kb/s
```

The video is in [DV format](https://en.wikipedia.org/wiki/DV_(video_format)) 720x480 (853x480 anamorphic). The audio is 32kHz 16-bit PCM. (The second audio track is just silence.)

Unfortunately, Resolve doesn't know how to read the DV files, so I needed to transcode to something else. I tried just muxing to a different container with ffmpeg but Resolve doesn't know the DV codec.

So I fiddled with [HandBrake](https://handbrake.fr/) to make a good mezzanine preset:

```
Preset:         DV Mezzanine 
Source:         .../Clip 35.dv
Destination:    .../Clip 35.mp4
Format:         MP4, Chapter Markers, Web Optimized
Range: 	        Title 35, Chapter 1
Dimensions:     Source: 720x480, Output: 720x480, Anamorphic: 853x480 Automatic
Video:          Encoder: H.264 (x264), Framerate: Same as source (variable), Constant Quality: 10.00 RF
Video Options:  Preset: slower, Tune: none, Options: tff=1, Profile: auto, Level: auto
Audio:          0: Unknown (pcm_s16le, 2.0 ch, 1024 kbps) ▸ Encoder: FLAC 16-bit, Mixdown: Stereo, Samplerate: Auto, Bitrate: -1 kbps
```

This is what it looks like in the GUI, with explanations:
![Summary tab](/images/dv-mezzanine/summary.png)

![Dimensions tab](/images/dv-mezzanine/dimensions.png)
I set Cropping, Anamorphic, and Final dimensions to "Automatic".

![Filters tab](/images/dv-mezzanine/filters.png)
DV is interlaced, and I want to keep it interlaced and let Resolve handle the deinterlacing.
I enabled the Interlace Detection filter, I think this might help with setting the metadata correctly. I did *not* enable the Deinterlace filter, because we want to keep it interlaced.

![Video tab](/images/dv-mezzanine/video.png)
There's no GUI checkbox to tell x264 to do interlaced encoding, so we add `tff=1` to the "Additional Options" box. This causes x264 to do top field first MBAFF encoding which is what we want (`bff=1` if your interlaced content is bottom field first).

I set Framerate to be same as source, Constant Qualtiy with RF=10, the "slower" preset and "auto" for Profile and Level. Tuning didn't seem appropriate, but if your source material calls for it knock yourself out.

![Audio Selection](/images/dv-mezzanine/audio_selection.png)
For the audio selection behavior, I checked auto passthru for all the formats that Resolve supports (according to the docs), with FLAC as the fallback (16-bit would have been sufficient probably, but I went with 24-bit). I made one track with "Auto Passthru" and 7.1 auto sample rate. When faced with the actual stereo PCM data this will fall back to FLAC and Stereo. If HandBrake supported PCM we could have passed that through but there's really no reason not to do FLAC.

The result is perceptually faithful, as close to the original as possible in all ways. Resolve recognizes that it's interleaved and automatically does the right thing (though you have options to tweak it of course).