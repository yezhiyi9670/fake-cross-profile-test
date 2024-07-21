# Fake Cross Profile Test

> **This app may cause irreversible damage to your system. USE AT YOUR OWN RISK.**

[**Download APK**](./app/release/FakeCrossProfileTest.apk)

## tl;dr

It is essentially a useless app named `com.android.cts.crossprofilepermissioncontrol`, signed using the universal test key.

This app is made to replicate a certain effect of the Cross Profile Test App. When installed on some OEM-customized ROMs, it will accidentally break some of the OEM's mods, and can hopefully remove some OEM shitfuckery and reveal some hidden options.

Normally, uninstalling this app and rebooting will revert all changes. However, as reported by some users, **some changes may be permanent and cannot be easily reverted without a factory reset**. USE AT YOUR OWN RISK.

## About Cross Profile Test

Cross Profile Test App is a part of [Google's CTS kit](https://source.android.google.cn/docs/compatibility/cts/downloads#android-13). In 2023, a video-maker [found that](https://www.bilibili.com/video/BV1Ph4y157Vu/?p=1) installing this app will break the ad-filled and potentially jailed APK installer in ColorOS and force the system into using vanilla Android APK installer instead. Other users also reported that many aspects of the user experience had been reverted to vanilla, for example, the appearance of the virtual buttons.

"Surprisingly, it crashed! But don't worry. The magic has been injected." the author said in the video. So what is that magic exactly? I tried to figure out with my own OnePlus 9R phone.

- First I found that one do not need to open the app and click on the button to make it work. Just install and reboot, then it will work.
- I read the source code of the app, and there's nothing special. It just tries to test the Cross Profile functionality, which has already become a standard in Android 12.
- I tried to unpack the app with apktool, remove some components and repack. I found that the Cross Profile Test is completely irrelevant with the issue, and an empty app that requests no permission and has virtually no java code or resources still works.
- Finally I spotted the difference. For the app to work, it must have package name `com.android.cts.crossprofilepermissioncontrol` and must be signed using the universal test key used in Android test builds. See the [test-key](./test-key/) folder.

However, I cannot explain HOW it breaks OEM mods. Perhaps I will do this later, or someone else can set out to find out.
