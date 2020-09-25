### android签名

秘钥：123456   **cordova01应用签名**

````js
keytool -genkey -v -keystore cordova01.keystore -alias cordova01.alias -keyalg RSA -validity 20000 -keystore /Users/fuaoqi/cordova01.keystore
````

**打包release版本** 

````js
// 打包release版本  cordova build android 也可以
cordova run android --release -- --keystore=./cordova01.keystore --storePassword=123456 --alias=cordova01.alias --password=123456
````



