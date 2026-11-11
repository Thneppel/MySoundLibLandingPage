---
title: "How to convert OPUS to WAV for video editing"
description: "Your editor won't take an .opus file? Here's what Opus is and three ways to convert it to WAV: MySoundLib, the free Audacity editor or one FFmpeg command, including batch conversion."
date: 2026-10-20
author: Thneppel
lang: en
slug: convert-opus-to-wav
tags:
  - audio formats
  - converter
  - video editing
image:
  path: /blog/convert-opus-to-wav/banner.webp
  alt: "Convert OPUS to WAV and get it into your editor: the MySoundLib converter turning .opus files into .wav over a dark editing timeline"
og_image_alt: "Convert OPUS to WAV and get it into your editor: the MySoundLib converter turning .opus files into .wav over a dark editing timeline"
---

If your video editor won't import an `.opus` file, convert it to WAV and import the WAV instead. You can do it in a few clicks with the converter built into MySoundLib, in the free Audacity editor, or with a single FFmpeg command if you don't mind the command line. All three work in batches, so a folder full of Opus files takes the same effort as one.

> The short version:
>
> - Opus is an open audio codec built for voice calls, chat and streaming, and not every video editor imports it.
> - Convert to WAV for editing. Converting can't bring back quality the Opus file already lost, but WAV won't lose any more.
> - In MySoundLib: add the files to the converter, pick WAV and click Convert all. In Audacity: File > Export Audio as WAV. With FFmpeg: `ffmpeg -i input.opus output.wav`.

## What is an Opus file?

Opus is "a totally open, royalty-free, highly versatile audio codec", standardized by the IETF as RFC 6716 ([opus-codec.org](https://opus-codec.org/)). It was designed for voice over IP, videoconferencing and in-game chat, and it's also used for storage and streaming. That's why Opus files tend to show up when you grab audio from a call, a chat app or a download, more than from a sound pack.

The format is fine for listening. The trouble starts when the file has to go into an edit: not every video editor imports `.opus`, and when yours doesn't, the file either fails with an error or doesn't appear in the import dialog at all.

## Why convert to WAV and not MP3

WAV is uncompressed, so converting to WAV doesn't throw away anything else. Opus is a lossy format, which means the conversion can't restore detail the Opus file already dropped, but it keeps everything that's left, in a format video editors import.

MP3 makes sense when file size matters more than quality, for example to send a rough cut to someone. For sound you're going to edit, mix and export again, WAV is the safer choice.

## Option 1: convert in MySoundLib

The converter in MySoundLib handles OPUS, FLAC, M4A, OGG and AIFF, and turns them into WAV or MP3.

1. Open the converter and add your `.opus` files. You can add one file or a whole folder.
2. Choose WAV as the output format.
3. Click Convert all. Each file shows its progress and is marked as converted when it's done.
4. Drag the converted WAV into your timeline, or search for it later with QuickSearch like any other sound.

The files never leave your computer: the conversion runs locally. More on the rest of the app on the [features page](https://mysoundlib.com/features.html).

## Option 2: convert with Audacity

Audacity is a free audio editor for Windows, macOS and Linux ([audacityteam.org](https://www.audacityteam.org/)), and a good choice if you'd rather click than type commands.

1. Open the `.opus` file in Audacity. If it won't open, install the optional FFmpeg library, which Audacity uses to import extra audio formats ([Installing FFmpeg](https://support.audacityteam.org/basics/installing-ffmpeg)).
2. Go to File > Export Audio.
3. Choose WAV as the format and set the sample rate to 48000 Hz. The default encoding is signed 16-bit PCM; pick a higher bit depth there if your project uses one.
4. Export, then import the WAV into your editor.

For many files at once, Audacity has Macros: build a macro with an export step, then use Tools > Apply Macro and choose Files to run it on a folder. The [Audacity manual](https://manual.audacityteam.org/man/macros.html) recommends processing no more than 500 files at a time.

## Option 3: convert with FFmpeg

FFmpeg is a free command-line tool that converts almost any audio or video format. Once it's installed, open a terminal in the folder with your file and run:

```
ffmpeg -i input.opus output.wav
```

Video projects usually run at 48 kHz, and you can set the sample rate and bit depth of the WAV explicitly:

```
ffmpeg -i input.opus -ar 48000 -c:a pcm_s24le output.wav
```

To convert every `.opus` file in a folder on Windows (PowerShell):

```
Get-ChildItem *.opus | ForEach-Object { ffmpeg -i $_.FullName -ar 48000 -c:a pcm_s24le ($_.BaseName + ".wav") }
```

On macOS or Linux:

```
for f in *.opus; do ffmpeg -i "$f" -ar 48000 -c:a pcm_s24le "${f%.opus}.wav"; done
```

FFmpeg is the right tool if you're comfortable in a terminal and convert files now and then. If converting is part of your editing routine, a converter inside your sound library saves you the trip to the terminal.

## Frequently asked questions

### Does converting OPUS to WAV improve the quality?

No. WAV keeps what the Opus file has, without adding new compression, but it can't recreate detail the Opus encoder removed. The WAV will be much bigger and sound the same.

### What sample rate should I use?

48 kHz is the usual rate for video, and Opus supports sampling rates up to 48 kHz. Converting to a 48 kHz WAV keeps things consistent with the rest of your project.

### What about other formats my editor refuses?

The same steps work for FLAC, M4A, OGG and AIFF. The MySoundLib converter takes all of them, and the FFmpeg commands above work if you change the file extension.

## About the author

I'm Thneppel, a video editor and the creator of MySoundLib. I work mostly in Premiere Pro and After Effects. More about me at [thneppel.com.br](https://thneppel.com.br). Questions or corrections about this post: [support@mysoundlib.com](mailto:support@mysoundlib.com).

## Sources

All pages last checked on November 10, 2026.

- Xiph.Org Foundation. [Opus Interactive Audio Codec](https://opus-codec.org/).
- Audacity. [audacityteam.org](https://www.audacityteam.org/), [Installing FFmpeg](https://support.audacityteam.org/basics/installing-ffmpeg) and [Macros](https://manual.audacityteam.org/man/macros.html).
