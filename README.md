# TLabWebViewVR-OculusIntegration-2022

## Overview
This sample is the minimum configuration for using TLabWebView with the MetaXR SDK. This includes searchbar example and javascript event (text area focus/focusout) example to toggle virtual keyboard visibility.

## Document
[document is here](https://tlabgames.gitbook.io/tlabwebview)

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

| Property | Value   |
| -------- | ------- |
| Platform | Android |

- Project Settings

| Property          | Value  |
| ----------------- | ------ |
| Color Space       | Linear |
| Minimum API Level | 29     |
| Target API Level  | 32     |


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
