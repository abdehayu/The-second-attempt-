# قبل الفجر – offline mobile app (Capacitor)

## One-time setup
```bash
npm install
npm run fonts            # bundles fonts locally (needed for offline use)
npm run setup:android    # any OS
npm run setup:ios        # macOS only
```
Before publishing, change `appId` in `capacitor.config.json` (e.g. `com.yourname.qablalfajr`).
Run `npm run sync` after every edit to `www/index.html`.

## Test
```bash
npm run android          # emulator or USB device
npm run ios              # Mac + Xcode
```
Check: airplane mode, sound button, volume slider, iPhone silent switch, backgrounding stops the music.

## Build
**Android** (Android Studio installed)
- Debug APK: `npm run build:apk` -> `android/app/build/outputs/apk/debug/app-debug.apk`
- Release: `npm run open:android`, then Build > Generate Signed Bundle / APK (AAB for Google Play). Back up your keystore.

**iOS** (Mac + Xcode)
- `npm run open:ios`, pick your Team under Signing & Capabilities.
- Product > Archive > Distribute App for an .ipa / TestFlight (paid Apple Developer account required).

## Manual iOS audio patch (only if patch-ios fails)
In `ios/App/App/AppDelegate.swift` add `import AVFoundation` and, in `didFinishLaunchingWithOptions` before `return true`:
```swift
try? AVAudioSession.sharedInstance().setCategory(.playback, mode: .default)
```

## Build the APK in the cloud (no tools to install)
Upload this folder to a new GitHub repository (branch `main`). Open the **Actions** tab, run **Build Android APK**, then download `app-debug-apk` from the finished run.
