# cordova-plugin-weibosdk
[![npm](https://img.shields.io/npm/v/cordova-plugin-weibosdk.svg)](https://www.npmjs.com/package/cordova-plugin-weibosdk)
[![npm](https://img.shields.io/npm/dm/cordova-plugin-weibosdk.svg)](https://www.npmjs.com/package/cordova-plugin-weibosdk)
[![platform](https://img.shields.io/badge/platform-iOS%2FAndroid-lightgrey.svg?style=flat)](https://github.com/iVanPan/cordova_weibo)
[![GitHub license](https://img.shields.io/github/license/mashape/apistatus.svg?style=flat)](https://github.com/iVanPan/cordova_weibo/blob/master/LICENSE)

A Cordova wrapper around the Sina WeiboSDK for Android and iOS. Provides access to ssoLogin, WeiboSharing etc... [简体中文](https://github.com/iVanPan/cordova_weibo/blob/master/README_ZH.md)  


## Feature
- Weibo SSO Login
- Weibo Logout
- Weibo Share (WebPage,Text,Image)
- Check Weibo Client is Installed

## Requirements
- Cordova Version 3.5+
- Cordova-Android >= 7.0
- Cordova-iOS >= 4.0			

## Installation
1. Add the plugin with your app ID:  
   ```cordova plugin add cordova-plugin-weibosdk --variable WEIBO_APP_ID=YOUR_WEIBO_APPID```
2. Add ```<preference name="REDIRECTURI" value="YOUR_WEIBO_REDIRECTURI" />``` in your config.xml. If you don't add this preference the default redirect URI is https://api.weibo.com/oauth2/default.html
3. (iOS) **Universal Link variables** — the plugin uses these for SDK 3.3+ and Associated Domains. Set them in your app’s **config.xml** under `<platform name="ios">` (the plugin does not inject them; the app owns these values):
   - **WEIBO_UNIVERSAL_LINK** — full Universal Link URL (e.g. `https://yourdomain.com/weibo/`). Required for Weibo SDK 3.3+.
   - **WEIBO_ASSOCIATED_DOMAIN** — domain only for the Associated Domains entitlement (e.g. `web.xiangyin.mobi`). The plugin injects `applinks:YOUR_DOMAIN` into the iOS project using this value.
   - Example in config.xml:
     ```xml
     <preference name="WEIBO_UNIVERSAL_LINK" value="https://web.xiangyin.mobi/weibo/" />
     <preference name="WEIBO_ASSOCIATED_DOMAIN" value="web.xiangyin.mobi" />
     ```
4. cordova build


## Notes
1. This plugin is required Cordova-Android version >= 4.0,so using Cordova 5.0 or higher is recommended
2. This plugin should be used after the deviceready event has been fired!!!				
3. ~~If Cordova version  <5.1.1,when two Cordova plugins are modifying “*-Info.plist” CFBundleURLTypes, only the first added plugin is getting the changes applied.so after installing plugin,please check the URLTypes in your Xcode project.You can find this issue [here](https://issues.apache.org/jira/browse/CB-8007).~~  Update:This Bug is fixed in last Cordova version(5.1.1)	


## Usage

### Weibo SSO Login
```Javascript
WeiboSDK.ssoLogin(function (args) {
   alert('access token is ' + args.access_token);
   alert('userId is ' + args.userId);
   alert('expires_time is ' + new Date(parseInt(args.expires_time)) + ' TimeStamp is ' + args.expires_time);
}, function (failReason) {
   alert(failReason);
});
```

### Weibo Logout
```Javascript
WeiboSDK.logout(function () {
   alert('logout success');
}, function (failReason) {
   alert(failReason);
});
```

### Weibo WebPage Share
```Javascript
var args = {};
args.url = 'https://cordova.apache.org/';
args.title = 'Apache Cordova';
args.description = 'This is a Cordova Plugin';
args.image = 'https://cordova.apache.org/static/img/pluggy.png';
WeiboSDK.shareToWeibo(function () {
   alert('share success');
}, function (failReason) {
   alert(failReason);
}, args);
```
### Weibo Image Share
```Javascript
var args = {};
args.image = 'https://cordova.apache.org/static/img/pluggy.png';
WeiboSDK.shareImageToWeibo(function () {
   alert('share success');
}, function (failReason) {
   alert(failReason);
}, args);
```
### Weibo Text Share
```Javascript
var args = {};
args.text = 'This is a Cordova Plugin';
WeiboSDK.shareTextToWeibo(function () {
   alert('share success');
}, function (failReason) {
   alert(failReason);
}, args);
```
### CheckClientInstalled
```Javascript
WeiboSDK.checkClientInstalled(function () {
   alert('client is installed');
}, function () {
   alert('client is not installed');
});
```
### GetUserInfo
```Javascript
var url = 'https://api.weibo.com/2/users/show.json?uid=' + usrid + '&&access_token=' + token;
http.get(url)
```

## Example			
1. install this plugin
2. backup www folder in your cordova project
3. replace www by example_www
4. cordova build & test

<div style="text-align:center"><img src="https://github.com/iVanPan/cordova_weibo/blob/master/ScreenShot.png?raw=true" alt="example" style="width:300px"></div> 

## About WeiboSdk
iOS plugin uses [weibo_ios_sdk](https://github.com/sinaweibosdk/weibo_ios_sdk) (3.3.x). You can download the latest SDK there; if you find any problem about the Weibo SDK, open an issue please.

## Contributing
Feel free to contribute                 

## License

**cordova-plugin-weibosdk** is released under the **MIT** license. See [LICENSE](https://github.com/iVanPan/cordova_weibo/blob/master/LICENSE) file for more information.

