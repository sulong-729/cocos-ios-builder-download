# Cocos Builder Duo Native

**Version 1.0.2 · iOS + Android APK · Apple Silicon Mac**

Build and run Cocos Creator native projects from one macOS desktop tool. Choose
**iOS** for Xcode / Simulator / iPhone, or **Android** for Gradle / APK / emulator /
Android phone. The installed application is currently named **cocos builder**.

## 1. Download the installer

- **[Download the macOS installer (.pkg)](https://media.githubusercontent.com/media/sulong-729/installer-cocos-builder-duo-native/dowload-v102/cocos-builder-1.0.2-macOS-arm64-development.pkg?download=1)**
- [Download its matching checksum (.sha256)](https://raw.githubusercontent.com/sulong-729/installer-cocos-builder-duo-native/dowload-v102/cocos-builder-1.0.2-macOS-arm64-development.pkg.sha256)
- [Read the complete installation and usage guide](USER_GUIDE.md)

Download both files. Use the direct installer link above: the repository ZIP and
small Git LFS pointer files are not installers. The real PKG is about **149.7 MB**.
Git LFS is not required when downloading through the direct link.

**Release status:** this is a development preview. The app is ad-hoc signed;
the PKG is unsigned and not Apple-notarized. macOS Gatekeeper may block it.
Administrator authorization during installation does not change this status.

## 2. Install on your Mac

1. Check that your Mac has an **Apple Silicon** chip and **macOS 14.4 or newer**.
   Open Apple menu → About This Mac to check. Intel Macs are not supported.
2. Save the PKG and SHA-256 file in the same folder, for example Downloads.
3. Open Terminal and verify the download:

   ```sh
   cd ~/Downloads
   shasum -a 256 -c cocos-builder-1.0.2-macOS-arm64-development.pkg.sha256
   ```

   Continue only when the filename is followed by **OK**. If it does not match,
   download the matching pair again.
4. Open the PKG in Finder. Follow macOS Installer and authorize the system-wide
   installation if asked.
5. Open **Applications → cocos builder**.

Python, Qt and QR support are included. Install the platform build tools below
separately. If macOS refuses this development build, see
[installation troubleshooting](USER_GUIDE.md#installation-problems).

## 3. Prepare the platform you need

| For both platforms | For iOS | For Android |
| --- | --- | --- |
| Install the exact Cocos Creator version in the game's `package.json` → `creator.version`. | Install full Xcode, finish first-launch setup and select its Command Line Tools. | Install Android Studio, SDK Platform, Build Tools, Platform Tools, NDK and a compatible JDK. |
| Open the game in Cocos and save a build task for the chosen platform. | Install a compatible Simulator runtime, or prepare iPhone trust, Developer Mode and development signing. | For an emulator also install Android Emulator, Command-line Tools and a system image. |

A saved Android task is enough for Android; an iOS task is not required.
The app does not automatically download missing Cocos or platform components.

## 4. First Android build and run

1. Add/select the Cocos project root in the sidebar. It contains `package.json`
   and `assets/`; do not choose `assets/` or a generated build directory.
2. Open **Android**. Expand **Công cụ Android** and select your installed Studio,
   SDK, NDK and Java Home. Run **Kiểm tra công cụ** and resolve any setup notices.
3. Select a saved Android task. Expand **Cocos Android Build Config** and check
   scenes, startup scene, Package ID, ABI and Debug mode.
4. Choose **Máy ảo Android**, select an AVD and use its green power icon to boot.
   Wait until ready. **Refresh** prefers a running emulator; green dots identify
   running rows. For a phone choose **Điện thoại thật** and connect by USB or Wi-Fi.
5. Click **Build & Run**. The tool exports Cocos → builds an APK → installs it on
   the selected device → launches it. Use **Build APK** to build without a device.
6. Watch the shared log panel. Picking a running device starts Logcat automatically,
   even before Run. Changing the selected device changes the log source.

[Full Android setup, USB, QR and pairing-code instructions](USER_GUIDE.md#android-build-and-run).

## 5. First iOS build and run

1. Select the project, open **iOS**, then **Cài đặt**.
2. Select the saved Cocos iOS task and check the Creator path and Bundle ID.
   For an iPhone also select the Apple Team ID and prepare signing in Xcode.
3. Choose Simulator or iPhone mode. Refresh and select a compatible destination.
4. Leave native-only mode off for the first build. Click **Build & Run**.
5. Wait for export, Xcode compilation and launch. Check both the log and the
   game window before considering the run successful.

**Updating an existing iOS game:** normal Run / Build & Run preserves an already
installed copy. Build the changes first, then use **Clean & Run** if you accept
uninstalling the selected game and deleting its device data. Android normally
uses reinstall/update (`adb install -r`) instead. The two platforms differ.

[Full iOS preparation and deployment instructions](USER_GUIDE.md#ios-build-and-run).

## 6. Which button should I use?

| Goal | iOS | Android |
| --- | --- | --- |
| Compile only, no device needed | Build | Build APK |
| Compile and launch on the selected device | Build & Run | Build & Run |
| Run a compatible build already on the Mac | Run | Run APK đã build |
| Delete installed app/data and reinstall | Build first, then Clean & Run | Clean & Run; reads/validates the APK before removal |
| Read runtime logs | Independent Simulator log controls | Automatic Logcat when a running device is selected |

Clean & Run requires confirmation. A successful build is not proof of a
successful install, and launch success is not proof that gameplay is stable.

## Help and limitations

The [full guide](USER_GUIDE.md) covers dependency errors, Java/Gradle mismatch,
missing devices, log colors, stale builds, settings and removal.

This release was exercised with Cocos 3.7.3 and an ARM64 Android emulator through
export/build/install/launch; automatic Logcat was verified. Physical Android QR
pairing and AVD creation/deletion still need native-device verification.
Windows/Linux hosts, Intel Mac installers, Creator 2.x, Android AAB output and
App Store / Play Store publishing are not supported.

Source: [sulong-729/cocosBuilderSrc](https://github.com/sulong-729/cocosBuilderSrc).
This download repo keeps the newest installer on **`dowload-v102`**, with its
checksum and guides. It does not publish Release/tag downloads.
