# ArtCraft-Downloader User Guide

Version 0.3.0 · Copyright © 2026 [DoggByte](https://doggbyte.com) · [License](LICENSE.txt) · [Changelog](CHANGELOG.md) · [Copyright and notices](COPYRIGHT.md)

---

## Contents

1. [What it does](#1-what-it-does)
2. [Getting started in five minutes](#2-getting-started-in-five-minutes)
3. [Installing](#3-installing)
4. [How the downloads are organized](#4-how-the-downloads-are-organized)
5. [Command reference](#5-command-reference)
6. [Choosing what to download](#6-choosing-what-to-download)
7. [Recipes](#7-recipes)
8. [Keeping your collection up to date](#8-keeping-your-collection-up-to-date)
9. [Reading the output](#9-reading-the-output)
10. [Checking file integrity](#10-checking-file-integrity)
11. [Troubleshooting](#11-troubleshooting)
12. [Limitations](#12-limitations)
13. [Frequently asked questions](#13-frequently-asked-questions)
14. [Uninstalling](#14-uninstalling)
15. [Getting help](#15-getting-help)
16. [License](#16-license)

---

## 1. What it does

ArtCraft-Downloader is a small command-line program that downloads the installers and archives of the **Craft apps** published by storytold on GitHub, and files them into a tidy folder tree: one folder per operating system, then one per app, then one per version.

The 14 supported apps (the 13 Craft apps and the ArtCraft Launcher, which is released from storytold's `craft-launcher` repository; its name works as `artcraft-launcher` or `craft-launcher`):

| App | | App | |
|---|---|---|---|
| PhotoCraft | | DeckCraft | |
| VectorCraft | | CADCraft | |
| FilmCraft | | GridCraft | |
| LightCraft | | WordCraft | |
| PdfCraft | | SoundCraft | |
| EffectCraft | | DesignCraft | |
| FigCraft | | ArtCraft-Launcher | |

What you get:

- **One command to fetch everything**, or just the apps, versions, operating systems and CPU types you choose.
- **Safe to run again and again.** Anything you already have is skipped; only new releases are downloaded.
- **Resumable.** If your connection drops, run it again and it continues where it stopped.
- **Verified.** New downloads are checked against the checksums published with each release.
- **A single file.** No installer, no Python, no other software needed.
- **Free.** Free to use for any purpose, including at work (see [section 16](#16-license)). It is not for sale.

What it does *not* do: it does not install the apps for you, it does not modify your system, and it does not delete anything. It only creates folders and downloads files into the folder you point it at.

> **Independent tool.** ArtCraft-Downloader is made by DoggByte and is not affiliated with storytold or the ArtCraft apps. It downloads files that storytold publishes publicly on GitHub; those files remain subject to their own terms. See [COPYRIGHT.md](COPYRIGHT.md).

---

## 2. Getting started in five minutes

1. **Download the program** for your computer from the [Releases page](https://github.com/DoggByte/artcraft-downloader/releases/latest) (see [section 3](#3-installing) if you are not sure which one).
2. **Open a terminal** (Terminal on macOS and Linux, PowerShell on Windows) in a folder where you want the downloads to go, and make sure you have free disk space (the full set of all 14 apps is roughly **17 GB** or more).
3. **Run it.** For example, to download only PhotoCraft:

   ```
   artcraft-downloader --apps photocraft
   ```

   On Linux and macOS you will usually type `./artcraft-downloader` and on Windows `.\artcraft-downloader.exe`; [section 3](#3-installing) explains why.

4. **Wait for it to finish.** You will see lines like:

   ```
   [PhotoCraft] v0.9.0: 26 assets
   [PhotoCraft] downloading SHA256SUMS.txt
   [PhotoCraft] downloading photocraft-0.9.0-freebsd-x86_64.tar.gz
   ...
   [PhotoCraft] done: 0 failed downloads, 0 checksum problems
   ```

5. **Look in the folder.** You now have `Windows/PhotoCraft/0.9.0/`, `Linux/PhotoCraft/0.9.0/`, and so on, filled with the release files.

To download all 14 apps, run it with no options:

```
artcraft-downloader
```

To see every option: `artcraft-downloader --help`.

---

## 3. Installing

There is nothing to install. ArtCraft-Downloader is one file. You just download it, make it runnable, and run it.

### 3.1 Which file do I need?

Every release on the [Releases page](https://github.com/DoggByte/artcraft-downloader/releases) contains these files:

| File | Use it on |
|---|---|
| `artcraft-downloader-windows-x64.exe` | Windows 10 or 11 on a normal Intel/AMD PC (most computers) |
| `artcraft-downloader-windows-arm64.exe` | Windows 11 on an ARM PC (for example Snapdragon laptops) |
| `artcraft-downloader-macos-universal` | Any Mac, Intel or Apple Silicon (macOS 11 or newer on Apple Silicon, 10.13 or newer on Intel) |
| `artcraft-downloader-linux-x86_64` | Linux on an Intel/AMD 64-bit PC |
| `artcraft-downloader-linux-aarch64` | Linux on a 64-bit ARM computer (Raspberry Pi 4 and 5 with a 64-bit OS, ARM servers) |
| `SHA256SUMS.txt` | Checksums for the files above (see [3.6](#36-optional-verify-your-download)) |
| `LICENSE.txt` | The license ([section 16](#16-license)) |

Not sure what CPU you have?

- **Windows:** open *Settings → System → About* and look at *System type* ("x64-based processor" or "ARM-based processor").
- **macOS:** the universal file works on every Mac, so you do not need to know.
- **Linux:** run `uname -m`. `x86_64` means the x86_64 file; `aarch64` or `arm64` means the aarch64 file.

There are no builds for 32-bit systems or for RISC-V computers.

### 3.2 Give it a simple name (recommended)

The examples in this guide use the short name `artcraft-downloader`. After downloading, rename the file to that (on Windows: `artcraft-downloader.exe`). Keep the long name if you prefer; just use it wherever the guide says `artcraft-downloader`.

### 3.3 Linux

```
cd ~/Downloads
mv artcraft-downloader-linux-x86_64 artcraft-downloader
chmod +x artcraft-downloader          # makes the file runnable (needed once)
./artcraft-downloader --version
```

> **Why `./`?** Your shell only runs programs it finds in your `PATH`. The current folder is not in it, so you must say where the file is: `./` means "in this folder". If you forget it you get `command not found`.

To run it from anywhere without `./`, put it in a folder that is on your `PATH`:

```
mkdir -p ~/.local/bin
mv artcraft-downloader ~/.local/bin/
artcraft-downloader --version         # now works from any folder
```

(On most distributions `~/.local/bin` is already on your `PATH` after you log in again. If not, add `export PATH="$HOME/.local/bin:$PATH"` to `~/.bashrc`.)

### 3.4 macOS

```
cd ~/Downloads
mv artcraft-downloader-macos-universal artcraft-downloader
chmod +x artcraft-downloader
./artcraft-downloader --version
```

If macOS says the program *"cannot be opened because the developer cannot be verified"* (it does this for files downloaded with a browser or received over AirDrop, because the program is not notarized by Apple), do one of:

- In Terminal: `xattr -d com.apple.quarantine artcraft-downloader`, then run it again.
- Or in Finder: right-click the file, choose *Open*, and confirm. After that it runs normally.

Files copied with `scp`, `rsync` or a USB drive are not affected.

### 3.5 Windows

1. Download `artcraft-downloader-windows-x64.exe` (or the arm64 file) and rename it to `artcraft-downloader.exe`.
2. Put it in a folder of your choice, for example `C:\Tools`.
3. Open **PowerShell** (right-click the Start button → *Terminal* or *Windows PowerShell*) and run:

   ```
   cd C:\Tools
   .\artcraft-downloader.exe --version
   ```

   (`.\` means "in this folder". Command Prompt works too; there you can leave it out.)

If Windows shows *"Windows protected your PC"* (SmartScreen), click **More info → Run anyway**. This appears because the program is not code-signed, not because anything is wrong with it. If you downloaded it with a browser and want to avoid the prompt, right-click the file → *Properties* → tick *Unblock* → *OK*.

**Optional: run it from any folder.** Add the folder to your `PATH`: press the Windows key, type *environment variables*, choose *Edit the system environment variables* → *Environment Variables…* → select *Path* under your user → *Edit* → *New* → enter `C:\Tools` → *OK*. Open a new PowerShell window afterwards.

### 3.6 (Optional) Verify your download

The release includes `SHA256SUMS.txt`. To make sure your copy is exactly what was published, compare its SHA-256 fingerprint with the one in that file.

- **Linux:** `sha256sum artcraft-downloader-linux-x86_64` (or `sha256sum -c --ignore-missing SHA256SUMS.txt` with the original file names in the same folder).
- **macOS:** `shasum -a 256 artcraft-downloader-macos-universal`
- **Windows (PowerShell):** `Get-FileHash .\artcraft-downloader-windows-x64.exe -Algorithm SHA256`

The long hexadecimal string printed must match the line for your file in `SHA256SUMS.txt`. Do this *before* renaming the file, or compare against the right line.

### 3.7 Where should I run it from?

The program writes into the **current folder** by default: it creates `Windows`, `Linux`, `macOS`, `FreeBSD` and `Cross-Platform` there. Either `cd` to the folder where you want your collection, or point it somewhere with `--dest`:

```
artcraft-downloader --dest /mnt/storage/artcraft
```

Choose a drive with enough room: the full set is about 17 GB, and every new version adds more.

---

## 4. How the downloads are organized

Everything is filed as:

```
<OS folder>/<App>/<version>/<release files>
```

For example, after downloading PhotoCraft 0.9.0:

```
Windows/
  PhotoCraft/
    0.9.0/
      photocraft-0.9.0-windows-x64.msi
      photocraft-0.9.0-windows-x64-portable.zip
      photocraft-0.9.0-windows-arm64.msi
      ...
Linux/
  PhotoCraft/
    0.9.0/
      photocraft-0.9.0-linux-x86_64.AppImage
      photocraft-0.9.0-linux-x86_64.deb
      photocraft-0.9.0-linux-aarch64.rpm
      ...
macOS/
  PhotoCraft/
    0.9.0/
      photocraft-0.9.0-macos-universal.dmg
      photocraft-cli-0.9.0-macos-universal.zip
FreeBSD/
  PhotoCraft/
    0.9.0/
      photocraft-0.9.0-freebsd-x86_64.tar.gz
Cross-Platform/
  PhotoCraft/
    0.9.0/
      photocraft-web-0.9.0.zip
      SHA256SUMS.txt
```

### What goes in each OS folder

| Folder | What is in it |
|---|---|
| `Windows` | `.msi` installers and portable `.zip` builds (x64, x86, arm64) |
| `Linux` | `.AppImage` (with a `.zsync` update file), `.deb`, `.rpm`, `.flatpak` and `.tar.gz` for x86_64 and aarch64, plus `.tar.gz`/`.deb`/`.rpm` for riscv64 |
| `macOS` | the universal `.dmg` installer, and a command-line `.zip` |
| `FreeBSD` | a `.tar.gz` for x86_64 |
| `Cross-Platform` | the web build (`.zip`) and the release's `SHA256SUMS.txt` |

The exact set varies a little between apps (some apps have an extra server package, some lack a RISC-V `.deb` or `.rpm`). The program simply downloads whatever the release contains.

### Good to know

- **Version folders sit side by side.** When a new version comes out, it gets its own folder (`0.10.0` next to `0.9.0`). Old versions are never touched or deleted by this program.
- **The version has no leading `v`.** The GitHub release `v0.9.0` is stored as `0.9.0`.
- **The checksum file lives in `Cross-Platform`**, even though it describes files that are stored in the other folders.
- **Folder names are fixed.** `Windows`, `Linux`, `macOS`, `FreeBSD`, `Cross-Platform` and the app names always use this exact capitalization. On Linux and macOS (case-sensitive disks) a differently spelled folder such as `windows` would be treated as a different folder.
- **The program creates all folders itself**, as it needs them. You can start in an empty folder.

---

## 5. Command reference

```
artcraft-downloader [options] [App ...]
```

With no options, it downloads the **latest release of all 14 apps**, for **every platform and architecture**, into the **current folder**.

### Options

| Option | What it does |
|---|---|
| `-a`, `--apps LIST` | Download only these apps. A comma-separated list; can be repeated. Names are not case-sensitive. `--apps=photocraft` also works. |
| `App ...` | App names written without an option do the same as `--apps`: `artcraft-downloader photocraft figcraft`. |
| `-r`, `--release VERSION` | Download this version instead of the latest, for example `0.8.2` or `v0.8.2`. Needs `--apps`. A version can also be set per app as `App=VERSION`. |
| `-o`, `--os LIST` | Download only the files for these platforms: `windows`, `linux`, `macos`, `freebsd`, `cross-platform`. Alias: `--platform`. |
| `--arch LIST` | Download only the files for these CPU types: `x64`, `arm64`, `x86`, `riscv64`, `universal`. Alias: `--architecture`. |
| `--format LIST` | Download only these installer types: `deb`, `rpm`, `appimage`, `flatpak`, `snap`, `msi`, `exe`, `portable`, `dmg`, `pkg`, `tar`, `web`, `cli`. Alias: `--type`. |
| `--native` | Download only what fits the computer you run it on: its platform, CPU type and installer type ([6.6](#66-this-computer---native)). |
| `--dest DIR` | The folder to write into (default: the current folder). It is created if it does not exist. |
| `--verify` | Re-check every selected file against the release's checksums, even if nothing new was downloaded. |
| `--list` | Print the 14 app names and exit. |
| `-V`, `--version` | Print the program version and copyright, then exit. |
| `-h`, `--help` | Print a summary of the options, then exit. |

Options that take a value accept either a space or an equals sign: `--dest D:\Archive` and `--dest=D:\Archive` are the same. Short options (`-a`, `-r`, `-o`) need a space.

### Lists

`--apps`, `--os`, `--arch` and `--format` accept several values separated by commas, and you can also repeat the option:

```
--apps photocraft,figcraft
--apps photocraft --apps figcraft
```

Spaces after the commas are fine if you put the whole list in quotes (`--apps "photocraft, figcraft"`). Naming something twice is harmless. The word `all` for `--os`, `--arch` or `--format` means "no filter".

### Platform names

| You type | Meaning |
|---|---|
| `windows` (or `win`) | files in the `Windows` folder |
| `linux` | files in the `Linux` folder |
| `macos` (or `mac`, `osx`, `darwin`) | files in the `macOS` folder |
| `freebsd` (or `bsd`) | files in the `FreeBSD` folder |
| `cross-platform` (or `cross`, `web`) | the web build and checksum file in `Cross-Platform` |

### Architecture names

| You type | Meaning |
|---|---|
| `x64` (or `x86_64`, `amd64`) | 64-bit Intel/AMD |
| `arm64` (or `aarch64`) | 64-bit ARM (Apple Silicon, Raspberry Pi, Windows on ARM) |
| `x86` (or `i386`, `i686`, `32bit`) | 32-bit Intel/AMD (Windows only) |
| `riscv64` (or `riscv`) | 64-bit RISC-V (Linux only) |
| `universal` | the macOS universal build |

### Installer type names

| You type | Meaning |
|---|---|
| `deb` (or `debian`) | Debian, Ubuntu and similar: `.deb` packages |
| `rpm` | Fedora, openSUSE and similar: `.rpm` packages |
| `appimage` | Linux AppImages (and their `.zsync` update files) |
| `flatpak`, `snap` | Flatpak and Snap packages |
| `msi`, `exe` | Windows installers |
| `portable` (or `zip`) | The portable Windows `.zip` builds |
| `dmg`, `pkg` | macOS disk images and installer packages |
| `tar` (or `tarball`, `tar.gz`, `tgz`) | Linux and FreeBSD `.tar.gz` archives |
| `web` | The web build |
| `cli` | The macOS command-line zip |

### Exit codes

| Code | Meaning |
|---|---|
| `0` | Everything succeeded (including "nothing to do"). |
| `1` | At least one download failed, a checksum did not match, or a release/version could not be found. |
| `2` | The command line was wrong (unknown option, app, platform, architecture or installer type, a missing value, or `--release` without `--apps`). Nothing was downloaded. |

---

## 6. Choosing what to download

You can combine any of the switches; each one narrows the result further.

### 6.1 Apps - `--apps`

```
artcraft-downloader --apps photocraft
artcraft-downloader -a photocraft,figcraft,gridcraft
artcraft-downloader photocraft figcraft          # same as above, without the option name
```

Run `artcraft-downloader --list` to see the exact names. An unknown name is rejected before anything is downloaded.

### 6.2 Versions - `--release`

By default you get the **latest** release, which is whatever GitHub marks as the latest (pre-releases are not counted as "latest"). To get a specific version instead:

```
artcraft-downloader --apps photocraft --release 0.8.2
artcraft-downloader -a photocraft -r v0.8.2           # the leading v is optional
```

`--release` always needs `--apps`, because version numbers differ from app to app (PhotoCraft is at 0.9.0 while FigCraft is at 0.6.0). For different versions of several apps, write the version after the name:

```
artcraft-downloader -a pdfcraft=0.7.1 -a deckcraft=0.6.1
artcraft-downloader -a pdfcraft=0.7.1,photocraft          # photocraft = latest
```

If a version does not exist, the program tells you which ones do:

```
[SoundCraft] ERROR release '9.9.9' not found. Available: v0.7.0, v0.6.1, v0.5.0, v0.4.0, v0.3.0
```

(The list shows the most recent releases GitHub displays on the first page.) You can download pre-release versions the same way if you know the tag, for example `--release 0.1.1-rc.4`.

### 6.3 Platforms - `--os`

```
artcraft-downloader --os windows
artcraft-downloader --os linux,macos
```

Only the folders you choose are created. The release's `SHA256SUMS.txt` is always downloaded too (it is tiny) so your files can be verified, which means a `Cross-Platform/<App>/<version>/` folder holding just that file will also appear.

### 6.4 CPU architecture - `--arch`

```
artcraft-downloader --arch x64
artcraft-downloader --arch arm64
```

Things to know:

- `x64` means 64-bit only. 32-bit Windows files are `x86` and are *not* included by `x64`; ask for them explicitly (`--arch x64,x86`).
- macOS *universal* files run on both Intel and Apple Silicon, so they are kept whether you ask for `x64`, `arm64` or `universal`.
- Files that mention no CPU type at all, namely the web build in `Cross-Platform`, are *not* removed by `--arch`. To leave them out as well, add `--os windows,linux,macos` (or whichever platforms you want).
- If a release has nothing that matches (for example `--os freebsd --arch arm64`), that app is reported and skipped; it is not an error.

### 6.5 Installer types - `--format`

```
artcraft-downloader --format deb
artcraft-downloader --format deb --arch x64
artcraft-downloader --format rpm,appimage
```

Use this when you only want one kind of installer, for example the `.deb` packages for a Debian or Ubuntu computer. The first line fetches the Debian packages of every app, for every CPU type; the second only the 64-bit Intel/AMD ones.

Things to know:

- Files of any other type are skipped, including files whose type the program does not recognise. `SHA256SUMS.txt` is always fetched so the downloads can be verified.
- `--format` looks at the file type only. It does not pick a platform for you, but each type belongs to one platform anyway (`deb` is always Linux, `msi` always Windows).
- An AppImage's `.zsync` update file counts as `appimage`.
- Which types exist depends on the app. If a release has none of the type you asked for, that app is reported and skipped; it is not an error.

### 6.6 This computer - `--native`

```
artcraft-downloader --native
```

Looks at the computer it is running on and downloads only the files that fit it, for every app. The program prints what it chose, for example `native: Linux, x64, deb`.

| Running on | Platform | Installer type |
|---|---|---|
| Debian, Ubuntu, Linux Mint and other Debian-based Linux | `linux` | `deb` |
| Fedora, RHEL, CentOS, openSUSE and similar | `linux` | `rpm` |
| Any other Linux | `linux` | `appimage` |
| Windows | `windows` | `msi` |
| macOS | `macos` | `dmg` |
| FreeBSD | `freebsd` | `tar` |

The CPU type is the one of the computer (`x64`, `arm64`, and so on).

Things to know:

- It is a shortcut for typing `--os`, `--arch` and `--format` yourself. Anything you give explicitly wins: `--native --format appimage` downloads AppImages instead of `.deb` files, and `--native --arch all` keeps every CPU type.
- If you name another platform with `--os`, the installer type is not guessed, because it would not fit that platform.
- The Linux type comes from `/etc/os-release`. If that file cannot be read, you get AppImages, which run on any distribution.
- If the program cannot tell what your computer is, it stops with a message and downloads nothing.

### 6.7 Combining them

```
artcraft-downloader --os windows --arch x64
artcraft-downloader -a photocraft -r 0.8.2 --os linux,macos --arch arm64
```

The first line fetches the 64-bit Windows files of the latest release of every app. The second fetches the Linux and macOS files for ARM of PhotoCraft 0.8.2.

You can add more later: running the same command again with another platform adds its files to the same version folder and does not re-download what you already have.

---

## 7. Recipes

**Download everything, once**

```
artcraft-downloader --dest /mnt/storage/artcraft
```

**Download just what my own computer needs** (64-bit Windows, all apps)

```
artcraft-downloader --os windows --arch x64
```

**Download the Linux installers for a Raspberry Pi**

```
artcraft-downloader --os linux --arch arm64
```

**Get an older version of one app**

```
artcraft-downloader --apps photocraft --release 0.8.2
```

**Get several apps at pinned versions**

```
artcraft-downloader -a pdfcraft=0.7.1 -a deckcraft=0.6.1 -a gridcraft=0.6.1
```

**Update my collection** (fetch only releases I do not have yet)

```
artcraft-downloader --dest /mnt/storage/artcraft
```

**Check that nothing in my collection is damaged**

```
artcraft-downloader --verify --dest /mnt/storage/artcraft
```

**See what would be available before committing disk space**

```
artcraft-downloader --apps photocraft --release 0.0.0
```

This is a trick, not a feature: the program refuses the non-existent version and lists the versions that do exist, without downloading anything.

**Mirror to an external drive**

```
artcraft-downloader --dest /Volumes/Backup/artcraft          # macOS
artcraft-downloader --dest D:\ArtCraft                        # Windows
```

---

## 8. Keeping your collection up to date

Run the same command whenever you like. For each app it asks GitHub for the latest release, and:

- if you already have it, it says `already downloaded, skipped` and moves on (this takes a second or two per app);
- if there is a newer version, it creates a new version folder and downloads the files.

Older versions stay where they are.

### Run it automatically

Always give the scheduled job a full path and an explicit `--dest`, because scheduled tasks do not start in your usual folder.

**Linux or macOS (cron)**: run `crontab -e` and add a line such as this one, which checks every Sunday at 03:00 and keeps a log:

```
0 3 * * 0  /home/me/.local/bin/artcraft-downloader --dest /mnt/storage/artcraft >> /home/me/artcraft-downloader.log 2>&1
```

**Windows (Task Scheduler)**: from a Command Prompt, create a weekly task:

```
schtasks /Create /SC WEEKLY /D SUN /ST 03:00 /TN "artcraft-downloader" /TR "C:\Tools\artcraft-downloader.exe --dest D:\ArtCraft"
```

(You can also create the task by hand in the *Task Scheduler* app: *Create Basic Task*, a weekly trigger, and *Start a program* with the program and `--dest ...` as arguments.)

Use the exit code to detect problems: `0` means all good, anything else means look at the log (see [section 5](#exit-codes)).

---

## 9. Reading the output

Each app prints a short report. Here is what the lines mean.

| Line | Meaning |
|---|---|
| `[App] v0.9.0: 26 assets` | The release found, and how many files it contains. |
| `[App] v0.9.0: 26 assets, 12 for x64` | Same, with how many files match your `--os`/`--arch` filters (and the filters, as in `2 for Windows, arm64`). |
| `[App] downloading <file>` | A file is being downloaded. Large files take a while; there is no progress bar. |
| `[App] 0.9.0 already downloaded, skipped` | Everything you asked for is already in place. Nothing was done. |
| `[App] 0.9.0 has no files for the selected platform/architecture, skipped` | The release exists but contains nothing matching your filters. |
| `[App] done: 0 failed downloads, 0 checksum problems` | The app finished and was checked. This is the "all good" line after a download. |
| `[App] FAILED <file>: <reason>` | A file could not be downloaded even after several attempts. Run the program again. |
| `[App] CHECKSUM PROBLEM <file>` | The file is missing or does not match the published checksum. See [section 10](#10-checking-file-integrity). |
| `[App] no SHA256SUMS.txt, skipped verification` | The release does not include a checksum file, so nothing could be verified. |
| `[App] ERROR <message>` | The app could not be processed (for example the release was not found). The other apps continue. |

If one app fails, the program carries on with the others and exits with code `1` at the end.

---

## 10. Checking file integrity

Every release publishes a `SHA256SUMS.txt` listing the expected fingerprint of each file. ArtCraft-Downloader checks your files against it:

- **automatically**, whenever it downloaded something new for an app, and
- **on demand**, for everything you select, with `--verify`.

```
artcraft-downloader --verify                       # whole collection, latest versions
artcraft-downloader --verify -a photocraft -r 0.8.2
```

`--verify` reads every selected file completely, so it takes a while on a big collection.

If a file is reported as a **CHECKSUM PROBLEM**:

1. Delete that file.
2. Run the same command again. The program notices the file is missing and downloads it fresh.

It does not delete or replace a damaged file by itself. A file that exists is always trusted unless you use `--verify`.

When you used `--os`/`--arch`, only the files you selected are checked; files you chose not to download are not reported as missing.

---

## 11. Troubleshooting

| Problem | Likely cause and fix |
|---|---|
| `command not found` (Linux/macOS) | The current folder is not on your `PATH`. Run it as `./artcraft-downloader`, or move it to a folder on your `PATH` ([3.3](#33-linux)). |
| `'artcraft-downloader' is not recognized` (Windows) | Same reason. Use `.\artcraft-downloader.exe` in PowerShell, or add its folder to `PATH` ([3.5](#35-windows)). |
| `Permission denied` (Linux/macOS) | The file is not marked runnable: `chmod +x artcraft-downloader`. If it still fails, the file may be on a drive mounted without permission to run programs (a USB stick, or a `noexec` mount). Copy it to your home folder. |
| `cannot execute binary file` / `Exec format error` | Wrong download for your CPU. Check with `uname -m` and pick the matching file ([3.1](#31-which-file-do-i-need)). |
| macOS: "cannot be opened because the developer cannot be verified" | Remove the download flag with `xattr -d com.apple.quarantine artcraft-downloader`, or right-click → *Open* ([3.4](#34-macos)). |
| Windows: "Windows protected your PC" | Choose *More info → Run anyway*, or right-click the file → *Properties* → *Unblock* ([3.5](#35-windows)). |
| `unknown app 'xyz'` | A typo in an app name. `artcraft-downloader --list` shows the valid names. |
| `unknown platform` / `unknown architecture` / `unknown installer type` | Use one of the names in [section 5](#platform-names). |
| `--release needs --apps` | Version numbers differ per app, so say which app: `-a photocraft -r 0.8.2`. |
| `release '1.2.3' not found. Available: ...` | That version does not exist for that app. Pick one from the list shown. |
| `latest release lookup failed` or `asset listing failed` (mentioning status code 429 or 403) | GitHub is limiting your requests (often after many runs in a short time, or on a shared network). Wait a few minutes and run again. |
| `latest release lookup failed` with a connection error | No internet connection, a firewall, or a proxy. The program connects directly to `github.com` and does not use proxy settings ([12](#12-limitations)). |
| `FAILED <file>` | A network problem or timeout. Run the program again; finished files are kept and the interrupted one resumes. |
| It stops with an error about writing a file | Usually the disk is full or the folder is read-only. Free some space or pick a different `--dest`. |
| `<file>.part` files are left over | A download was interrupted. Run the program again to finish it; the `.part` file is renamed when complete. You can delete leftover `.part` files if you do not want them. |
| `CHECKSUM PROBLEM` | See [section 10](#10-checking-file-integrity). |
| It says `skipped` but I expected a download | You already have that version. To see what is on GitHub, ask for a version that does not exist; the error lists the real ones ([7](#7-recipes)). |
| A file I want is missing from the folder | It may be filtered out by `--os`/`--arch`, or the release simply does not contain it. Run once without filters, or look at the release on GitHub. |
| Nothing happens for a long time | Large files (hundreds of MB) take a while and there is no progress bar. Watch the folder: a growing `.part` file means it is working. |

---

## 12. Limitations

Being upfront about what version 0.3.0 does not do:

- **No proxy support.** The program needs a direct connection to `github.com`. Proxy environment variables (`HTTPS_PROXY` and similar) are ignored.
- **One download at a time.** Files are fetched one after another. You can run separate copies for different apps in different terminals if you want parallel downloads, but give each one *different apps* and do not point two copies at the same app and folder at the same time.
- **No free-space check.** The program does not check your disk before downloading. The full set is about 17 GB.
- **No progress bar.** You see a line per file, not a percentage.
- **Fixed list of apps.** Only the 14 apps in [section 1](#1-what-it-does) are supported.
- **Existing files are trusted.** A file that is already in place is not re-downloaded, even if it is damaged, unless you delete it ([section 10](#10-checking-file-integrity)).
- **It does not delete.** Old versions and leftover files are never removed.
- **Not code-signed.** The Windows and macOS programs trigger a one-time confirmation prompt.
- **No self-update.** To update ArtCraft-Downloader itself, download the new version from the Releases page and replace the file. See the [Changelog](CHANGELOG.md) for what changed.

---

## 13. Frequently asked questions

**Is it really free? Can I use it at work?**
Yes to both. It is free for any purpose, including commercial and business use, and you may share unmodified copies for free. What you may not do is sell it. Section 16 has the details.

**Can I put it in my own tool, installer or documentation?**
Yes, if you credit the author ("Includes ArtCraft-Downloader by DoggByte (https://doggbyte.com)") and do not sell it as a product of its own. Using it only for yourself or inside your own organization needs no credit. See [section 16](#16-license).

**Is this safe to run?**
It only creates folders and files inside the folder you point it at, and downloads from `github.com`. It does not install anything, change settings, or delete files. You can read the checksums of the program itself in the release's `SHA256SUMS.txt`.

**Does it install the apps?**
No. It only downloads their installers and archives. You install them the usual way afterwards (double-click the `.msi`, open the `.dmg`, install the `.deb`, and so on).

**Do I need a GitHub account or a token?**
No. The files are public, and the program does not log in.

**Why are the files not named like the folders?**
The file names are exactly as published by the app's authors. The folders around them are the organization this tool adds.

**Can I move or rename the folders afterwards?**
You can move the whole collection anywhere. If you rename folders (`Windows` → `windows`, or a version folder), the program will not recognize them and will download those files again next time.

**Can I download only one file?**
Not a single file, but you can narrow it to one app, one version, one platform and one CPU type, which in practice is a handful of files, for example `-a photocraft -r 0.9.0 --os windows --arch x64`.

**Why does `--arch x64` still give me a `.zip` from `Cross-Platform`?**
That file (the web build) has no CPU type in its name, so `--arch` cannot judge it. Add `--os windows,linux,macos` to exclude it.

**What does "latest" mean exactly?**
The release GitHub marks as the latest for that app. Pre-releases and drafts are not "latest"; ask for them by version if you need one.

**Can I run it on a server without a screen?**
Yes. It is a plain command-line program with text output and meaningful exit codes ([section 8](#8-keeping-your-collection-up-to-date)).

**Where do I report a bug or ask for a feature?**
See [section 15](#15-getting-help).

---

## 14. Uninstalling

Delete the `artcraft-downloader` file. That is all: it installs nothing and keeps no settings. Your downloaded collection is just ordinary files and folders; delete or keep them as you like. If you added the program's folder to your `PATH`, remove that entry too.

---

## 15. Getting help

- **Website:** <https://doggbyte.com>
- **Releases, documentation and issue reports:** <https://github.com/DoggByte/artcraft-downloader>

When reporting a problem, please include the output of `artcraft-downloader --version`, your operating system and CPU type, the exact command you ran, and the text of any error lines.

---

## 16. License

ArtCraft-Downloader is Copyright © 2026 [DoggByte](https://doggbyte.com) and is released under the **ArtCraft-Downloader Free Use License**. The full terms are in [`LICENSE.txt`](LICENSE.txt), which is what counts; this is a plain-language summary.

**You may**

- use it for any purpose, including at work and for commercial projects, at no cost;
- install it on as many computers as you like;
- give unmodified copies to other people for free, as long as you include the license and copyright notices;
- run it as part of your own paid work (for example, to prepare downloads for a client), as long as you are not charging for the tool itself.

**You may not**

- sell, resell, rent, or lease it, or charge for it or for access to it;
- put it behind a paywall, subscription, or a download that requires payment;
- remove or alter the copyright and license notices, or pass it off as your own work;
- say or imply that the author endorses your product.

**If you include it in something you share**

If you bundle, embed, or ship ArtCraft-Downloader as part of another product, package, installer, script collection, service or documentation that you make available to others (free or paid), you must credit the author somewhere reasonably visible (an About or Credits screen, a README, or a download page), with wording at least as clear as:

> Includes ArtCraft-Downloader by DoggByte (https://doggbyte.com)

and keep the license with it. If the larger product is sold, ArtCraft-Downloader must not be the main thing being sold or be priced as a separate item. Using it only for yourself or inside your own organization needs no credit.

**No warranty, no liability**

The software is provided "as is", without warranty of any kind. The author is not responsible for any damage or loss that results from using it, including lost or corrupted files, full disks, data or bandwidth charges, or lost profit. You use it at your own risk.

**Not covered by this license**

- The apps the tool downloads belong to their owners and are subject to their own terms; you are responsible for complying with them.
- ArtCraft-Downloader is not affiliated with, or endorsed by, storytold or the ArtCraft apps.
- The open-source libraries inside the program are licensed to you under their own terms; see [THIRD_PARTY_LICENSES.txt](THIRD_PARTY_LICENSES.txt).

If you would like to do something the license does not allow (for example, to sell or bundle the tool commercially), contact the author through <https://doggbyte.com>.

See also [COPYRIGHT.md](COPYRIGHT.md).
