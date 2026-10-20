# Cocos Builder Duo Native 1.0.2 — Download and User Guide

Cocos Builder Duo Native supports native **iOS and Android APK** workflows.

This branch, **`dowload-v102`**, contains the installer, checksum, and English
user documentation. Application source is maintained in a separate public
repository. Downloads are distributed from this branch without a Release/tag.

## Download

- [Download the macOS installer (.pkg)](https://media.githubusercontent.com/media/sulong-729/cocos-builder-duo-native/dowload-v102/cocos-builder-1.0.2-macOS-arm64-development.pkg?download=1)
- [Download the checksum (.sha256)](https://raw.githubusercontent.com/sulong-729/cocos-builder-duo-native/dowload-v102/cocos-builder-1.0.2-macOS-arm64-development.pkg.sha256)
- [Read the full User Guide](USER_GUIDE.md)

The installer is stored with Git LFS because it exceeds GitHub's normal Git
file limit. The direct installer link above returns the actual package. If
browsing files on GitHub, open the PKG and choose **Download raw file**. Do not
use a small LFS pointer file or the repository's ZIP archive as the installer.

## Requirements and supported scope

| Area | Support |
| --- | --- |
| Mac hardware | Apple Silicon M-series, arm64; Intel Macs are not supported |
| macOS | 14.4 or newer for this app; the selected Xcode may require newer macOS |
| Engine | Creator 3.x projects with a saved iOS or Android task; compatibility work mainly targets 3.7.x/3.7.3 |
| Destinations | iPhones / iOS Simulators; Android emulators and USB / Wi-Fi phones |
| Build actions | Build, Build & Run, Run an existing build, Clean & Run |
| Tools | Per-project build options, scenes/orientations, export cache, Simulator management, Simulator logs, and native .ips report inspection |
| Included runtime | Python 3.15, Qt/PySide6 and QR support; no separate installation required |

Not supported: Windows/Linux, Android AAB output, Creator 2.x, Mac Intel installer,
App Store/TestFlight upload, automatic prerequisite installation, or independent
live iPhone console capture. Every Creator 3.x version/custom template has not
been device-verified. The current UI is mainly Vietnamese; this guide is English.

## Install

1. Download the PKG and checksum using the links above.
2. Keep both files in the same folder. In Terminal, open that folder and run:

   ```sh
   shasum -a 256 -c cocos-builder-1.0.2-macOS-arm64-development.pkg.sha256
   ```

3. Confirm it reports `OK`, then open the `.pkg` and follow macOS Installer.
4. Authorize the system-wide installation when macOS asks.
5. Launch **cocos builder** from `/Applications`.

**This is a development preview: ad-hoc signed app, unsigned installer, and no
Apple notarization.** Gatekeeper may block it or suggest moving it to Trash.
Administrator authorization does not override that check. A normal trusted
release requires Developer ID signing and Apple notarization by the maintainer.

## Prepare a project

1. Install full Xcode, open it once, finish setup/license prompts, and select
   its Command Line Tools in Xcode Settings → Locations.
2. Install the exact Creator version from the game's `package.json` (`creator.version`).
3. Open the game in Cocos and save an iOS build task with scenes/startup scene.
4. For Simulator, install a compatible iOS runtime. Creator 3.7.x needs x86_64
   runtime support (Universal Runtime/Rosetta can be required on Apple Silicon);
   Creator 3.8+ Simulator builds select arm64.
5. For iPhone, pair/trust the Mac, enable Developer Mode, and establish working
   development signing in Xcode.

## Use the iOS tool

1. Choose/drop the Cocos project root containing `package.json` and `assets/`.
2. Open **Cài đặt** (Settings), select the saved iOS task, and check the Creator path.
3. Set the Bundle ID and, for iPhone builds, the correct 10-character Apple Team ID.
4. Expand **Cocos iOS Build Config** to check Debug/Release, scenes/start scene,
   orientations, output/cache, and other supported Cocos settings.
5. Choose Simulator or iPhone mode, refresh devices, and select the destination.
6. Click the action appropriate for your workflow:

| Action | Behavior |
| --- | --- |
| Build | Export when needed and compile on the Mac; no install/launch, no selected device needed |
| Build & Run | Build, then install only when absent and launch; preserves an existing installed app |
| Run | Use a compatible existing build; no export/compile, preserves an installed app |
| Clean & Run | After confirmation, delete the selected app and its data, install the built copy, and launch |

Build first after changing game code/assets. Use **Clean & Run** when you want
to replace an existing installation and accept deleting its game data. Leave
native-only mode off after asset/script changes; force Cocos export if needed.

Stopping independent log observation disconnects the observer without intentionally
stopping the game. Deep native debugging still requires Xcode/LLDB.

## Android APK workflow

1. Install the project's Cocos Creator version and Android Studio with SDK,
   NDK, Build Tools, Platform Tools and a compatible JDK. Emulator management
   additionally needs Command-line Tools, Emulator and an installed system image.
2. Select the project, open Android and select a saved Cocos Android task.
3. Select the installed Studio / SDK / NDK / JDK and check the build configuration.
   Compatible installed Java is chosen automatically for Gradle / SDK utilities.
4. Pick an emulator or phone in the single device dropdown. Refresh prefers a
   running emulator; green indicators identify running devices. Power icons are
   green to boot and red to shut down. USB, Wi-Fi code and QR pairing are available
   in phone mode. Missing components show installation guidance.
5. Use Build APK, Build & Run or Run APK. Clean & Run asks before removing data.
   Picking a running device automatically streams Logcat to the shared log panel,
   including during builds. Errors are red, warnings yellow, SDK/NDK parameters
   green, and ordinary logs white. Tab badges show work and device counts.

This release was tested with Cocos 3.7.3 on an ARM64 Android emulator through
export, APK build, installation and launch. Automatic device Logcat was verified.
Physical QR pairing and AVD creation/deletion remain unverified on real devices.

## Troubleshooting and detailed instructions

The [full User Guide](USER_GUIDE.md) explains all settings, output paths, cached
exports, device preparation, Simulator controls, logs, crash reports, uninstall,
and common errors. Build/launch success does not verify gameplay stability.

Installer SHA-256:

```text
ee9dda6de54bc3ac79ea0c54217a7edad8de44367fb1ea253bed4e925d1a08bf
```

## Clone instead of downloading from the browser

Install Git LFS first, then:

```sh
git lfs install
git clone --branch dowload-v102 --single-branch https://github.com/sulong-729/cocos-builder-duo-native.git
cd cocos-builder-duo-native
git lfs pull
shasum -a 256 -c cocos-builder-1.0.2-macOS-arm64-development.pkg.sha256
```

Without Git LFS, Git can check out only a small pointer file rather than the
149.7 MB installer. Browser users can simply use the direct download link above.
