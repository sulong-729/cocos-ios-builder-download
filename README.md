# Cocos iOS Builder — Downloads

A macOS desktop tool for building and running Cocos Creator 3.x projects on iOS.
This repository contains user documentation for the **newest build only**. The application development repository is private and separate.

The download branch is intentionally named **`dowload`**.

## Current download

**Version 1.0.1 — Development Preview**

Download the installer and its matching SHA-256 file from the
[1.0.1 release page](https://github.com/sulong-729/cocos-ios-builder-download/releases/tag/v1.0.1).

- Installer: `cocos-builder-1.0.1-macOS-arm64-development.pkg`
- Checksum: `cocos-builder-1.0.1-macOS-arm64-development.pkg.sha256`
- Target: **Apple Silicon arm64, macOS 14.4 or newer**
- Status: **ad-hoc signed app; unsigned installer; not notarized by Apple**

Gatekeeper may block this preview on another Mac or suggest moving it to Trash.
Administrator authorization in Installer does not override that check. A normal
signed distribution requires Developer ID signing and Apple notarization by the
maintainer. This preview must not be described as a notarized release.

The installer is a Release asset because it exceeds GitHub's 100 MiB normal-file
limit. The branch contains only user documentation; the installer and checksum are Release assets.
Do not download GitHub's automatic “Source code” archives to install the tool.

## Supported scope

| Area | Support |
| --- | --- |
| Mac | Apple Silicon M-series; macOS 14.4+; the selected Xcode can require newer macOS |
| Engine | Creator 3.x projects with a saved iOS build task; compatibility work primarily targets 3.7.x |
| Devices | Physical iPhone and compatible iOS Simulator runtimes |
| Build actions | Build, Build & Run, Run an existing build, Clean & Run |
| Configurations | Debug/Release, scenes/start scene, orientations, cache, supported Cocos iOS options |
| Simulator tools | Create, boot, show, shut down, restart, and delete the selected Simulator |
| Diagnostics | Build logs, independent Simulator logs, `.ips` crash report inspection with matching local symbols |
| Included runtime | Python 3.15 and Qt/PySide6 |

Not provided: Intel Mac installer, Windows/Linux, Android, Creator 2.x,
App Store/TestFlight upload, independent live iPhone console capture, or automatic
installation of Xcode/Cocos/runtimes. Every Creator 3.x version/custom template
has not been device-verified. The app interface is currently mainly Vietnamese;
these instructions are English.

## Install

1. Download the `.pkg` and `.sha256` files together.
2. From their download folder, verify integrity:

   ```sh
   shasum -a 256 -c cocos-builder-1.0.1-macOS-arm64-development.pkg.sha256
   ```

3. Open the installer and follow macOS Installer.
4. Authenticate through the system administrator dialog when requested.
5. Open **cocos builder** in `/Applications`.

## First project

1. Install full Xcode, open it once, finish setup, and select its Command Line Tools.
2. Install the exact Creator version from the game's `package.json`.
3. Save an iOS task in Cocos at least once.
4. Choose/drop the Cocos project root in the tool.
5. Open Settings, choose the task, and configure the Bundle ID and, for iPhone,
   Apple Team ID and working development signing.
6. Select an iPhone or compatible Simulator and click Build & Run.

For Creator 3.7.x Simulator builds, the selected runtime must support x86_64;
Apple Silicon hosts can need a Universal iOS Runtime and Rosetta. Creator 3.8+
Simulator builds select arm64 in the current implementation.

Normal Run and Build & Run preserve an existing installed app. To deploy a new
build when the Bundle ID is already installed, build first and use **Clean &
Run**. That action deletes the selected app and its data after confirmation.

## Detailed documentation

- [Full User Guide](USER_GUIDE.md)
- [Installer SHA-256](https://github.com/sulong-729/cocos-ios-builder-download/releases/download/v1.0.1/cocos-builder-1.0.1-macOS-arm64-development.pkg.sha256)

The user guide covers all settings, build/cache behavior, Simulator management,
logs/crash reports, prerequisites, troubleshooting, and uninstall instructions.
The newest release is the only supported download; previous build assets are
removed when a newer release has been verified.
