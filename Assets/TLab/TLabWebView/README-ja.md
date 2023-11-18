# TLabWebView  

Unityで動作するWebViewのプラグイン．WebViewの結果をTexture2Dとして表示できます  
- ハードウェアアクセラレーションによる描画も取得可能  
- キーボード入力をサポート  
- ファイルのダウンロードをサポート  
- javascriptの実行に対応  

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/tlabaltoh)

## スクリーンショット  
Android13, Adreno 619で実行した画面  


<img src="Media/tlab-webview.png" width="256">


## 動作環境
OS: Android 10 ~ 13  
GPU: Qualcomm Adreno 505, 619  
Unity: 2021.23f1  

## スタートガイド
### 必要な要件
- Unity 2021.3.23f1  
- [TLabVKeyborad](https://github.com/TLabAltoh/TLabVKeyborad)
### インストール
リポジトリをクローン，またはリリースからダウンロードし，UnityのAssetフォルダに配置してください
### セットアップ
1. Build Settingsからプラットフォームを Androidに変更  
2. Project Settings --> Player --> Other Settings に以下のシンボルを追加(ビルド時に使用)
```
UNITYWEBVIEW_ANDROID_USES_CLEARTEXT_TRAFFIC
```
```
UNITYWEBVIEW_ANDROID_ENABLE_CAMERA
```
```
UNITYWEBVIEW_ANDROID_ENABLE_MICROPHONE
```
- Color Space: Linear
- Graphics: OpenGLES3
- Minimux API Level: 23 
  
- Assets/Plugins/Android/AndroidManifest.xmlを作成し，以下のテキストをコピーする
```xml
<?xml version="1.0" encoding="utf-8"?>
<manifest
    xmlns:android="http://schemas.android.com/apk/res/android"
    package="com.unity3d.player"
    xmlns:tools="http://schemas.android.com/tools">
    <application>
        <activity android:name="com.unity3d.player.UnityPlayerActivity"
                  android:theme="@style/UnityThemeSelector">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />
                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
            <meta-data android:name="unityplayer.UnityActivity" android:value="true" />
        </activity>
    </application>

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
</manifest>
```
3. TLabWebView/TLabWebView.prefab をシーンに追加
4. WebViewの設定を変更
TLabWebView.cs の設定項目(TLabWebView.prefab/WebView にある)  

<img src="Media/tlab-webview-settings.png" width="256">  

- Url: WebViewの初期化時にロードするURL  
- DlOption: ファイルをアプリケーションフォルダとダウンロードフォルダどちらにダウンロードするか  
- SubDir: アプリケーションフォルダにダウンロードする場合，```{Application folder}/{files}/{SubDir}```にダウンロードされる  
- Web (Width/Height): WebViewの解像度 (デフォルト 1024 * 1024)  
- Tex (Width/Height): Texture2Dの解像度 (デフォルト 512 * 512)  

## Scripting API
### Initialize
- public void Init(int webWidth, int webHeight, int tWidth, int tHeight, int sWidth, int sHeight, string url, int dlOption, string subDir, IntPtr texId)
- public bool IsInitialized()
- public void StartWebView()
### Update Frame
- public byte[] GetWebTexturePixel() <span style="color: red; ">(obsolete)</span>
- public IntPtr GetWebTexturePtr()
- public void UpdateFrame()
### Capture Element
- public void CaptureHTMLSource()
- public void CaptureElementById(string id)
- public string CurrentHTMLCaptured()
### Load URL
- public void LoadUrl(string url)
- public void LoadHTML(string html, string baseURL)
- public void GoForward()
- public void GoBack()
### Zoom In/Out
- public void ZoomIn()
- public void ZoomOut()
### User Agent
- public void CaptureUserAgent()
- public string GetUserAgent()
- public void SetUserAgent(string ua, bool reload)
### Evaluate Javascript
- public void EvaluateJS(string js)
### Touch Event
- public void TouchEvent(int x, int y, int eventNum)
### Key Event
- public void KeyEvent(char key)
- public void BackSpace()
### Clear Cache
- public void ClearCache(bool includeDiskFiles)
- public void ClearCookie()
- public void ClearHistory()

## お知らせ
- VRでのプレイに対応しました([link](https://github.com/TLabAltoh/TLabWebViewVR))

## リンク
[使用したJavaプラグインのソースコード](https://github.com/TLabAltoh/TLabWebViewPlugin)
