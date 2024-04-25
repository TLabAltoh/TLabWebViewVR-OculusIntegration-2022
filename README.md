# TLabWebViewVR-OculusIntegration-2022

## Overview
This sample is the minimum configuration for using TLabWebView with the MetaXR SDK.

## Document
[document is here](https://tlabgames.gitbook.io/tlabwebview)

## Note
<details><summary>please see here</summary>

### Oculus SDK Updated to Meta XR SDK
The Oculus SDK has now been updated for Oculus integration SDK to Meta XR All in One SDK, this sdk requires Unity Editor 2021.26f1 ~. Oculus SDK versions after 57 (Meta XR SDK) are managed by Unity Package Manager (UPM), but have near-compatibility between Oculus Integration and the Meta XR SDK. However, in the sample scene in this repository, the Meta XR SDK sample has been updated to no longer use the OVR Input Module and switched to Pointable Canvas Module based, because the UI implementation sample including the Oculus SDK is based on the Pointable Canvas Module and it's inappropriate to implement webview with the OVR Input Module as before. (2021/4/14)

### Module Management Policy Modified
The policy has been changed to manage libraries in the repository as submodules after commit ``` 4a7a833 ```. Please run ``` git submodule update --init ``` to adjust the commit of the submodule to the version recommended by the project.

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
