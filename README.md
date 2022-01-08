Redestribution README
=====================

This repository hosts the [state](https://github.com/FFmpeg/FFmpeg/tree/1eca11f81a0204acfc85748c5f8d3c95719d8bab) of the [FFmpeg](https://www.ffmpeg.org/) [source code](https://github.com/FFmpeg/FFmpeg) corresponding to the Prebuilt FFmpeg binaries in the releases section. It is a very outdated version of FFmpeg, however during testing this version produced the best output using the selected codecs and therefore was selected. These binaries are by default used by all of Dynamotivation’s applications which require their functionality. The functionality of these binaries has been extremely reduced to mere png to mp4 and gif conversions. However the binaries will not function without the [correct Windows 32 bit binary](https://github.com/cisco/openh264/releases/tag/v2.1.1) of [Cisco’s](https://www.cisco.com/) [OpenH264 Codec](https://www.openh264.org/) renamed to “libopenh264.dll” and placed in the same directory as the executables. The original FFmpeg README is located below and marked as such.

## Release binary licenses
The binaries are subject to the [LGPL 2.1](https://www.gnu.org/licenses/old-licenses/lgpl-2.1.html) and include zlib functionality under the [zlib license](https://zlib.net/zlib_license.html).
Cisco’s OpenH264 binary is additionally subject to [all of the binaries license terms](https://www.openh264.org/BINARY_LICENSE.txt) and not therefore must be downloaded seperately.

## Build Process and Configuration
To compile the binaries the [Media-autobuild Suite](https://github.com/m-ab-s/media-autobuild_suite) was used.

The /build/media-autobuild_suite.ini contained the following:
```
[compiler list] 
arch=2
license2=5
standalone=1
vpx2=2
aom=2
rav1e=2
dav1d=2
libavif=2
jpegxl=2
x2643=2
x2652=2
other265=2
svthevc=2
xvc=2
vvc=2
svtav1=2
svtvp9=2
flac=2
fdkaac=2
faac=2
exhale=2
mediainfo=2
soxB=2
ffmpegB2=3
ffmpegUpdate=3
ffmpegChoice=1
mp4box=2
rtmpdump=2
mplayer2=2
mpv=2
vlc=2
bmx=2
curl=2
ffmbc=2
cyanrip2=2
redshift=2
ripgrep=2
jq=2
jo=2
dssim=2
avs2=2
CC=2
cores=6
deleteSource=1
strip=1
pack=2
logging=1
updateSuite=2
timeStamp=1
ccache=2
noMintty=2
```

Meanwhile the /build/ffmpeg_options.ini contained the following:
```
--disable-everything
--disable-nvenc
--disable-avdevice
--disable-postproc
--enable-small
--enable-filter=scale
--enable-zlib
--enable-libopenh264
--enable-encoder=libopenh264
--enable-protocol=file
--enable-encoder=gif
--enable-decoder=png
--enable-muxer=mp4
--enable-muxer=gif
--enable-demuxer=image2
--disable-ffplay
--disable-ffprobe
```

To configure the utility in a way that compiles our chosen commit instead of the upstream FFmpeg version one must let the utility perform the self update and then abort the execution and modify files.

The /build/media-suite_compile.sh script contains multiple references to https://git.ffmpeg.org/ffmpeg.git which need to be exchanged for the URL to your chosen commit or in this case the URL to this repository. Some error may appear later on, however the compilation as described will succeede. The suite can be started again upon making these changes.

No other configuration files were modified.

## Support
No support will be provided for this repository or any repository involved in the compilation of the binaries.
Do NOT rely on this repository for your own projects. This repository mainly exists to comply with the [FFmpeg License](https://ffmpeg.org/legal.html) and thus will only be guaranteed to exist for 3 years after the last of Dynamotivation’s applications relying on it for export functionality releases. No concrete day will be decided for the termination of the (source code) portion as preservation of it and the learning process behind compiling the specific binaries are important.


FFmpeg README
=============

FFmpeg is a collection of libraries and tools to process multimedia content
such as audio, video, subtitles and related metadata.

## Libraries

* `libavcodec` provides implementation of a wider range of codecs.
* `libavformat` implements streaming protocols, container formats and basic I/O access.
* `libavutil` includes hashers, decompressors and miscellaneous utility functions.
* `libavfilter` provides a mean to alter decoded Audio and Video through chain of filters.
* `libavdevice` provides an abstraction to access capture and playback devices.
* `libswresample` implements audio mixing and resampling routines.
* `libswscale` implements color conversion and scaling routines.

## Tools

* [ffmpeg](https://ffmpeg.org/ffmpeg.html) is a command line toolbox to
  manipulate, convert and stream multimedia content.
* [ffplay](https://ffmpeg.org/ffplay.html) is a minimalistic multimedia player.
* [ffprobe](https://ffmpeg.org/ffprobe.html) is a simple analysis tool to inspect
  multimedia content.
* [ffserver](https://ffmpeg.org/ffserver.html) is a multimedia streaming server
  for live broadcasts.
* Additional small tools such as `aviocat`, `ismindex` and `qt-faststart`.

## Documentation

The offline documentation is available in the **doc/** directory.

The online documentation is available in the main [website](https://ffmpeg.org)
and in the [wiki](https://trac.ffmpeg.org).

### Examples

Coding examples are available in the **doc/examples** directory.

## License

FFmpeg codebase is mainly LGPL-licensed with optional components licensed under
GPL. Please refer to the LICENSE file for detailed information.

## Contributing

Patches should be submitted to the ffmpeg-devel mailing list using
`git format-patch` or `git send-email`. Github pull requests should be
avoided because they are not part of our review process and will be ignored.
