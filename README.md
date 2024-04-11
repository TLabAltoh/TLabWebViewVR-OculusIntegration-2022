# TLabWebViewVR-OculusIntegration-2022

## Overview
- Sample project for using TLabWebView with Oculus Integration
- This sample is the minimum configuration for using TLabWebView with the Oculus Integration.

## Document
[document is here](https://tlabgames.gitbook.io/tlabwebview)

## Note
<details><summary>please see here</summary>

### Issue 1 (Android Custom Manifest)

Unity 2021.1.* recommended adding the following to the manifest file

```xml
<!-- For Unity-WebView -->
<application android:allowBackup="true"/>
<application android:supportsRtl="true"/>
<application android:hardwareAccelerated="true"/>
<application android:usesCleartextTraffic="true"/>

<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.MICROPHONE" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />

<uses-feature android:name="android.hardware.camera" />
<uses-feature android:name="android.hardware.microphone" />
<!-- For Unity-WebView -->
```

However, this is not recommended for Unity 2022.1.* and later.
        Adding this caused a problem with the manifest file not being properly configured at build time.
        It is recommended not to add these items to Android Custom Manifest after Unity 2022.1.*. (Creating Custom Manifest itself is not a problem)

### Issue 2 (Android Custom Manifest)

When specifying OpenXR as the XR plugin provider, a part of the manifest is forcibly deleted and an error occurs in WebView. Therefore, it is recommended to specify Oculus as the plugin provider.

```xml
<!-- Error: net::ERR_CACHE_MISS -->
<uses-permission android:name="ANDROID.PERMISSION.INTERNET"/> <!-- Missing !! -->
```

### Issue 3 (After updating the repository, the built app crashes)

The specific cause of this problem is still unknown. Please delete the build cache (``` root/Library/Bee ```) and try building again.

### The policy has been changed to manage libraries in the repository as submodules

- Commit ``` f26c332 ``` If you cloned the project before, please clone the repository again.
- Use ``` git submodule update --init ``` to adjust the commit of the submodule to the version recommended by the project.

</details>

## Getting Started

### Requirements
- Unity Editor: 2022.3.19f1

### Installing
Clone the repository with the following command

```
git clone https://github.com/TLabAltoh/TLabWebViewVR-OculusIntegration-2022.git

cd TLabWebViewVR-OculusIntegration-2022

git submodule update --init
```

### Set up
- Build Settings

| Property      | Value   |
| ------------- | ------- |
| Platform      | Android |

- Project Settings

| Property          | Value     |
| ----------------- | --------- |
| Color Space       | Linear    |
| Graphics          | OpenGLES3 |
| Minimum API Level | 29        |
| Target API Level  | 32        |


- Add the following symbols to Project Settings --> Player --> Other Settings (to be used at build time)

```
UNITYWEBVIEW_ANDROID_SUPPORT_OCULUS
```
```
UNITYWEBVIEW_ANDROID_USES_CLEARTEXT_TRAFFIC
```
```
UNITYWEBVIEW_ANDROID_ENABLE_CAMERA
```
```
UNITYWEBVIEW_ANDROID_ENABLE_MICROPHONE
```

- XR Plug-in Management

| Property        | Value               |
| --------------- | ------------------- |
| Plugin Provider | Oculus (not OpenXR) |