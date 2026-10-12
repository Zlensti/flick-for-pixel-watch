# Flick for Pixel Watch

A free, experimental Pixel Watch app that dismisses one notification at a time with a middle-finger/thumb flick.

Wake and unlock your watch, open the notification list, and flick when the card you want to dismiss is centered. One recognized flick requests one dismissal. No snapping sound is needed.

**No recording or practice is required.** Flick includes a built-in gesture model. Grant the required permissions, tap **Turn on**, and wait for **Gestures on**. Optional personal teaching is available under Options.

## Early beta

Version **0.18.0-beta.1** includes a starter model learned from one wearer's gesture examples. It may miss another person's flicks or mistake ordinary movements for flicks. Accuracy across wearers, watch models, languages and software versions is not yet verified. Battery impact has not been measured.

A matching development build was tested on one Pixel Watch 3 in English. In the latest trial, three flicks produced exactly three dismissals, all three test cards cleared fluidly, and the other notifications were unchanged. The separately signed public APK has passed software and package checks, but its fresh-install flow has not yet been tested on a physical watch.

## Download

Get the APK from [Releases](https://github.com/Zlensti/flick-for-pixel-watch/releases), or choose the share ZIP for the APK, installation guide, privacy information and checksum. Install the APK directly on your watch using a computer and Wi-Fi. This is a sideloaded beta, not a Play Store listing.

## Install on the watch

1. Download and extract [Google Android Platform Tools](https://developer.android.com/tools/releases/platform-tools). Put the Flick APK in the extracted platform-tools folder. Connect the computer and watch to the same Wi-Fi network.
2. On the watch, open **Settings > System > About > Versions**. Tap **Build number** seven times. Menu wording can vary.
3. Open **Developer options**. Enable **ADB debugging** and **Wireless debugging**, then choose **Pair new device**.
4. Open a terminal in the platform-tools folder. Run the pairing command below using the address shown under Pair new device, and enter the six-digit code when asked.

```text
adb pair WATCH_IP:PAIRING_PORT
```

Return to the main Wireless debugging screen. Its connection port is usually different from the pairing port. Use that address for these commands:

```text
adb connect WATCH_IP:CONNECTION_PORT
adb devices
adb -s WATCH_IP:CONNECTION_PORT install -r Flick-0.18.0-beta.1.apk
```

Replace the address placeholders with your watch values. On macOS/Linux use `./adb`; in Windows PowerShell use `.\adb.exe`. Wait for **Success**, then open **Flick** from the watch app list. [Official Google connection instructions](https://developer.android.com/training/wearables/get-started/debug-wifi).

## Turn it on

1. Tap **Allow access**, or open **Options > Access & privacy**, and read the permission explanations.
2. Enable **Flick notification gestures** in Accessibility and **Flick notification access** where available. These are separate permissions.
3. Return to Flick, tap **Turn on**, and wait for **Gestures on**.

You do not need to record flicks or complete a practice session first.

If your watch has no notification-access settings screen, use this computer command:

```text
adb -s WATCH_IP:CONNECTION_PORT shell cmd notification allow_listener com.kevinruby.flicklab/com.kevinruby.flicklab.notifications.FlickNotificationListener
```

This grants notification access only. Accessibility and turning gestures on are separate steps. If Android shows a restricted-settings warning, see the included INSTALL.txt and [Google help](https://support.google.com/android/answer/12623953); watch menus vary. Once setup works, turn ADB debugging and Wireless debugging off. Flick does not need your computer or a network connection for daily use.

## Everyday use

Open notifications with a swipe up or your watch's supported system pinch gesture. Flick once when the desired card is centered. Flick does not add Google's pinch feature to watches that lack it.

The on/off choice is saved. Gestures pause while the screen is off, the watch is locked, or you record or practice. Incoming alerts briefly pause recognition to avoid mistaking their vibration for a flick. **Turn off** keeps gestures off. A system force-stop requires opening the app again.

## Optional personal gesture

If the built-in gesture does not suit you, **Options > Teach my gesture** lets you record your own flicks and ordinary movements. **Practice** counts recognized gestures without dismissing notifications. Neither is required to turn Flick on.

Existing personal training is preserved by compatible updates. Options can switch between the built-in gesture and a saved personal gesture without deleting recordings. Switching turns gestures off until you tap Turn on again. Start over turns gestures off and keeps old examples privately without using them.

## Permissions and privacy

- **Accessibility:** reads the visible notification list, including card text and app names, to identify the centered card and perform its dismissal or a rightward swipe.
- **Notification access:** Android grants broad access; Flick uses alert arrivals to avoid recognizing notification vibrations as flicks.
- Processing and optional personal recordings stay on your watch. Notification content is not saved or uploaded.
- The APK includes learned numeric gesture templates from one wearer, with permission to share them. It contains no raw wearer recordings or notification content.
- No account, ads, analytics service, Internet permission, camera, or microphone.

The share ZIP includes PRIVACY.txt with details. Uninstalling removes local training data. The public release APK cannot update an earlier debug-signed development build directly, so do not uninstall a trained development build just to switch versions.

## Feedback

Report your watch model, Wear OS version, watch language, and whether flicks are missed or normal movements trigger the app in [Issues](https://github.com/Zlensti/flick-for-pixel-watch/issues). Avoid including personal notification content.
