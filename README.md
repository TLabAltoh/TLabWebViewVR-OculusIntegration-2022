# TLabWebViewVR-OculusIntegration-2022

## Overview
This sample Unity project is the minimum configuration for using [```TLabWebView```](https://github.com/TLabAltoh/TLabWebView) (3D web browser / 3D WebView plugin) with the [```MetaXR SDK```](https://developers.meta.com/horizon/downloads/package/meta-xr-sdk-all-in-one-upm). This includes searchbar example and javascript event (text area focus/focusout) example to toggle virtual keyboard visibility.

[Document is here](https://tlabgames.gitbook.io/tlabwebview)  
[Snippets is here](https://gist.github.com/TLabAltoh/e0512b3367c25d3e1ec28ddbe95da497#file-tlabwebview-snippets-md)

> [!WARNING]
> Note that this project only works on Android devices; it will not display web pages when run on the Unity Editor.

> [!WARNING]
> Meta XR All-in-One SDK is having a reference error at version 74 (Please see [this forum](https://www.reddit.com/r/oculusdev/comments/1jn4l5k/error_implementing_meta_allinone_sdk/)), so I will keep version 72 for now.

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
Please see the setup section [here](https://github.com/TLabAltoh/TLabWebView?tab=readme-ov-file#set-up)

<details><summary>When using the OpenXR plugin</summary>

Please disable `Force Remove Internet Permission` from XR Plugin Manegement

<img src="Media/image.png" width="512"></img>

</details>