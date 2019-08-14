
## Android Studio

```bash
# JAVA环境变量
JAVA_HOME
C:\Program Files\Java\jdk1.8.0_91
JAVA_HOME_JRE
C:\Program Files\Java\jdk1.8.0_91\jre
CLASSPATH
%JAVA_HOME%\lib;%JAVA_HOME%\lib\tools.jar

# path
%JAVA_HOME%\bin
%JAVA_HOME%\jre\bin

# Android环境变量
ANDROID_HOME
C:\Users\LJW\AppData\Local\Android\Sdk

# path
%ANDROID_HOME%\tools
%ANDROID_HOME%\platform-tools

# 启动Android模拟器
C:\Users\LJW\AppData\Local\Android\Sdk\tools\emulator.exe -netdelay none -netspeed full -avd Pixel_2_API_27

java -version

adb
adb devices
android

# 连接网易MuMu模拟器
adb connect 127.0.0.1:7555
adb shell

# 连接夜神模拟器

# adb.exe 复制替换 nox_adb.exe
C:\Users\LJW\AppData\Local\Android\Sdk\platform-tools\adb.exe
D:\down\install\Nox\bin\nox_adb.exe

cd D:\down\install\Nox\bin
nox_adb.exe connect 127.0.0.1:62001
```


## Cordova

[官方文档](https://cordova.apache.org/docs/en/latest/)

```bash
yarn global add cordova

cordova platform add android
cordova build --release android
```

## Quasar

## 官方文档

- [Quasar 中文文档](http://www.quasarchs.com/guide/cordova-build-commands.html)
- [Cordova 文档](https://cordova.apache.org/docs/en/latest/guide/support/index.html)
- [dayjs 中文文档](https://github.com/iamkun/dayjs/blob/85785462f8/docs/zh-cn/API-reference.md)
- [正则表达式手册](http://tool.oschina.net/uploads/apidocs/jquery/regexp.html)

### 安装

```bash
yarn global add quasar-cli
quasar init ..
```

### 基础命令

```bash
init          Create a project folder
dev           Start a dev server for your App
build         Build your app for production
clean         Clean all build artifacts
new           Quickly scaffold page/layout/component/... vue file
mode          Add/remove Quasar Modes for your App
info          Display info about your machine and your App
serve         Create an ad-hoc server on App distributables
help          Displays this message
```

### 新建命令

```bash
quasar new [p|page] <page_file_name>
quasar new [l|layout] <layout_file_name>
quasar new [c|component] <component_file_name>
quasar new plugin <plugin_name>
quasar new [s|store] <store_module_name>

# Examples:

# Create src/pages/MyNewPage.vue:
quasar new p MyNewPage

# Create src/pages/MyNewPage.vue and src/pages/OtherPage.vue:
quasar new p MyNewPage OtherPage

# Create src/layouts/shop/Checkout.vue
quasar new layout shop/Checkout.vue
```

### WEB 开发命令

```bash
# 运行开发服务器(使用默认主题)
quasar dev

# 运行开发服务器(使用特定主题)
quasar dev -t mat
quasar dev -t ios

# 运行在特定端口
quasar dev -p 9090

# PWA模式
quasar dev -m pwa
```

### WEB 构建命令

```bash
# 构建生产版本
quasar build

# 构建生产版本(使用特定主题)
quasar build -t mat
quasar build -t ios

# PWA
quasar build -m pwa
```

### Android 开发命令

> 运行前先检查模拟器连接情况

```bash
adb devices
```

```bash
quasar dev -m cordova -T android -t mat
```

### Android 构建命令

#### 构建安卓 apk

```bash
quasar build -m cordova -T android -t mat
```

#### apk 文件目录

```bash
D:\WWW\app\708\708-app\src-cordova\platforms\android\app\build\outputs\apk\release
```

#### ~~生成 Android 密钥~~（仅首次构建运行）

```bash
keytool -genkey -v -keystore my-release-key.keystore -alias alias_name -keyalg RSA -keysize 2048 -validity 20000
```

#### 签名 apk

```bash
jarsigner -verbose -sigalg SHA1withRSA -digestalg SHA1 -keystore my-release-key.keystore app-release-unsigned.apk alias_name
```

> 密钥密码```123456```

#### zipalign 目录

```bash
C:\Users\LJW\AppData\Local\Android\Sdk\build-tools\28.0.3
```

#### zipalign 优化 apk

```bash
zipalign -v 4 D:\WWW\app\708\708-app\src-cordova\platforms\android\app\build\outputs\apk\release\app-release-unsigned.apk D:\WWW\app\708\708-app\src-cordova\platforms\android\app\build\outputs\apk\release\RuixinTreasure.apk
```

### IOS 开发命令

```bash
quasar dev -m cordova -T ios -t ios
```

### IOS 构建命令

```bash
quasar build -m cordova -T ios -t ios
```

