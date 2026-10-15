# ArtCraft-Downloader

**Download the latest releases of the ArtCraft "Craft" apps and keep them neatly organized, with one command.**

ArtCraft-Downloader is a small command-line program for Windows, macOS and Linux. It fetches the installers and archives of the Craft apps that storytold publishes on GitHub and files them as `OS / App / Version`, so you always know what you have, can pick exactly the platform and CPU type you need, and can keep older versions side by side.

By [DoggByte](https://doggbyte.com) · Copyright © 2026 DoggByte · [Changelog](CHANGELOG.md) · [User guide](USER_GUIDE.md)

```
$ artcraft-downloader --apps photocraft --os windows --arch x64
[PhotoCraft] v0.9.0: 26 assets, 2 for Windows, x64
[PhotoCraft] downloading SHA256SUMS.txt
[PhotoCraft] downloading photocraft-0.9.0-windows-x64-portable.zip
[PhotoCraft] downloading photocraft-0.9.0-windows-x64.msi
[PhotoCraft] done: 0 failed downloads, 0 checksum problems
```

## Supported apps

PhotoCraft · VectorCraft · FilmCraft · LightCraft · PdfCraft · EffectCraft · DesignCraft · FigCraft · WordCraft · SoundCraft · DeckCraft · CADCraft · GridCraft · ArtCraft-Launcher

## Features

- Latest release of every app with one command, or only the apps you name
- Any specific older version (`--release 0.8.2`), including different versions per app
- Only the platforms (`--os`) and CPU types (`--arch`) you need
- Skips what you already have; rerun it any time to pick up new releases
- Resumes interrupted downloads and verifies files against the published SHA-256 checksums
- One self-contained file: no installer, no Python, nothing else required
- Script-friendly exit codes for scheduled updates
- Free to use, including at work (see [License](#license))

## Download

Get the file for your computer from the **[latest release](https://github.com/DoggByte/artcraft-downloader/releases/latest)**:

| File | For |
|---|---|
| `artcraft-downloader-windows-x64.exe` | Windows 10/11 (Intel/AMD) |
| `artcraft-downloader-windows-arm64.exe` | Windows 11 on ARM |
| `artcraft-downloader-macos-universal` | macOS, Intel and Apple Silicon |
| `artcraft-downloader-linux-x86_64` | Linux, Intel/AMD 64-bit |
| `artcraft-downloader-linux-aarch64` | Linux, ARM 64-bit |

Compare your download with `SHA256SUMS.txt` from the same release if you want to verify it.

## Quick start

1. Download the file for your system and (optionally) rename it to `artcraft-downloader` (`artcraft-downloader.exe` on Windows).
2. On Linux and macOS make it runnable once: `chmod +x artcraft-downloader`.
3. In a terminal, in the folder where you want your collection, run it:

   ```
   ./artcraft-downloader --list                 # see the app names
   ./artcraft-downloader --apps photocraft      # download one app
   ./artcraft-downloader                        # download everything (about 17 GB)
   ```

   (Windows PowerShell: `.\artcraft-downloader.exe ...`)

The first run on macOS or Windows may ask you to confirm that you want to open a program from an unidentified developer; the [user guide](USER_GUIDE.md#3-installing) explains how.

## Common commands

```
artcraft-downloader                                         # latest of all apps
artcraft-downloader --apps photocraft,figcraft              # only these apps
artcraft-downloader --os windows --arch x64                 # only 64-bit Windows files
artcraft-downloader -a photocraft -r 0.8.2                  # a specific older version
artcraft-downloader -a pdfcraft=0.7.1 -a deckcraft=0.6.1    # different versions per app
artcraft-downloader --dest /mnt/storage/artcraft            # choose where files go
artcraft-downloader --verify                                # re-check files against checksums
artcraft-downloader --help                                  # every option
```

## Documentation

- **[User guide](USER_GUIDE.md)**: installation on each system, every option, recipes, scheduling, troubleshooting, limitations, FAQ
- **[Changelog](CHANGELOG.md)**: what changed in each version
- **[License](LICENSE.txt)** (free to use, not for sale, credit the author if you include it in your own work), **[copyright and notices](COPYRIGHT.md)**, and **[third-party licenses](THIRD_PARTY_LICENSES.txt)**

## About this repository

This repository publishes the compiled programs (in [Releases](https://github.com/DoggByte/artcraft-downloader/releases)) and their documentation. The source code is not published here. To report a problem or suggest a feature, open an issue on this repository and include the output of `artcraft-downloader --version`, your operating system, and the command you ran.

## License

ArtCraft-Downloader is **free to use** for any purpose, including commercial and business use, and you may share unmodified copies for free. You **may not sell or resell it**, or put it behind a paywall. If you include it in your own product, package or documentation that you share with others, **credit the author** ("Includes ArtCraft-Downloader by DoggByte (https://doggbyte.com)"). It comes with **no warranty**, and the author is not liable for any damage. The full, binding terms are in [`LICENSE.txt`](LICENSE.txt).

## Notice

ArtCraft-Downloader is an independent tool by DoggByte. It is not affiliated with, or endorsed by, storytold or the ArtCraft apps. It downloads files that storytold publishes publicly on GitHub; those files remain subject to their own terms.

Copyright © 2026 DoggByte. Free to use, not for sale; see the [license](LICENSE.txt) and [COPYRIGHT.md](COPYRIGHT.md).
