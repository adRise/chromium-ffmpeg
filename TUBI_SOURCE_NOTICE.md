# FFmpeg source for the Tubi Fire TV app

This repository is the source code of the FFmpeg library distributed in the Tubi app for
Amazon Fire TV (package `com.tubitv.ott`, version 10.39 and later). It is published to meet
the GNU Lesser General Public License, version 2.1 (see `COPYING.LGPLv2.1`).

## What this is

- Chromium's copy of FFmpeg, unmodified by Tubi:
  https://chromium.googlesource.com/chromium/third_party/ffmpeg
- Revision `dcdd0fa51b65a0b1688ff6b8f0cc81908f09ded2` (tag `chromium-ffmpeg-dcdd0fa51b65`).
  Every file in that commit is byte-identical to upstream; this notice is the only file Tubi added.
- Chromium's changes to FFmpeg are included; they live under `chromium/` and are described
  in `README.chromium`.

## How it is built

The library is compiled as part of a Chromium-based browser engine embedded in the app,
using Chromium's GN build with:

```
media_use_ffmpeg    = true
ffmpeg_branding     = "Chrome"
is_component_ffmpeg = true
```

- Licence configuration: LGPL 2.1 (`CONFIG_GPL=0`, `CONFIG_NONFREE=0`, `CONFIG_VERSION3=0`),
  Chromium's default.
- Shipped as a separate shared library, `lib/armeabi-v7a/libffmpeg.so`, inside the APK.
- On Android ARM, FFmpeg's video decoders are not built; it provides container demuxing and
  audio decoding. Video is decoded by the device's hardware decoder.
