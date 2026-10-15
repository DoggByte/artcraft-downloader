# Changelog

All notable changes to ArtCraft-Downloader are recorded here.
The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and versions follow [Semantic Versioning](https://semver.org/).

## [Unreleased]

Nothing yet.

## [0.1.0] - 2026-10-15

First release.

### Added
- Downloads the latest release of the 13 Craft apps from storytold's public GitHub releases: PhotoCraft, VectorCraft, FilmCraft, LightCraft, PdfCraft, EffectCraft, DesignCraft, FigCraft, WordCraft, SoundCraft, DeckCraft, CADCraft and GridCraft.
- Organizes everything as `<OS>/<App>/<version>/` (`Windows`, `Linux`, `macOS`, `FreeBSD`, `Cross-Platform`) and creates the folders itself.
- `--apps` / `-a` (also plain app names): download only the apps you name. `--list` prints the valid names.
- `--release` / `-r`: download a specific version instead of the latest, either for all named apps or per app with `App=VERSION`. An unknown version prints the versions that exist.
- `--os` / `-o`: download only the files for some platforms (`windows`, `linux`, `macos`, `freebsd`, `cross-platform`).
- `--arch`: download only the files for some CPU architectures (`x64`, `arm64`, `x86`, `riscv64`, `universal`).
- `--dest`: choose the folder the files are written into.
- `--verify`: check downloaded files against each release's `SHA256SUMS.txt`. Checking also happens automatically after anything new is downloaded.
- `--version` / `-V` and `--help` / `-h`.
- Skips releases that are already downloaded, so rerunning the tool only fetches what is new.
- Interrupted downloads resume where they stopped (files are written as `.part` and renamed when complete), and each file is attempted up to 5 times automatically.
- Exit codes for scripting: `0` success, `1` a download, checksum, or release lookup failed, `2` invalid command line.
- Released under the ArtCraft-Downloader Free Use License (`LICENSE.txt`): free to use, including at work; free to share unmodified; credit the author when including it in your own work; not for sale; no warranty.
- Prebuilt single-file programs for Linux (x86_64 and aarch64), macOS (universal, Intel and Apple Silicon), and Windows (x64 and arm64), with no other software required.

### Known limitations
- Proxy settings are not used; the tool needs a direct connection to github.com.
- Downloads run one at a time, and free disk space is not checked beforehand.
- The Windows and macOS programs are not code-signed, so Windows SmartScreen and macOS Gatekeeper may ask you to confirm the first run.
- Only the 13 apps above are supported.

[Unreleased]: https://github.com/DoggByte/artcraft-downloader/compare/v0.1.0...HEAD
[0.1.0]: https://github.com/DoggByte/artcraft-downloader/releases/tag/v0.1.0
