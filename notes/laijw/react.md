# React

## create-react-app

[React 中文文档](https://www.reactjscn.com/)

```bash
# create-react-app
yarn global add create-react-app
create-react-app my-app
cd my-app/
npm start
```

## python

```bash
手动安装 python2.7 或 yarn global add --production windows-build-tools
yarn global add node-gyp
npm config set python python2.7
npm config set msvs_version 2015

# 添加环境变量
PYTHON
C:\Python27\python.exe

# path
C:\Python27\
C:\Python27\Scripts
```

## node_sass

```bash
# 根目录新建.npmrc
phantomjs_cdnurl=http://cnpmjs.org/downloads
sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
registry=https://registry.npm.taobao.org
```

## mirror-config-china

```bash
yarn global add mirror-config-china
```

> License for package Android SDK Build-Tools 28.0.2 not accepted

```bash
cd C:\Users\LJW\AppData\Local\Android\Sdk\tools\bin
sdkmanager --licenses
```

## React Native

[React Native 中文文档](https://reactnative.cn/)

```bash
yarn global add react-native-cli
react-native init rn_demo --version 0.59.9
react-native init rn_rematch_demo --template with-rematccode 
react-native init rn_redux_demo --template rematch-redux
react-native run-android

# To run your app on iOS:
cd D:\WWW\567\a567
react-native run-ios
- or -
Open ios\a567.xcodeproj in Xcode
Hit the Run button

# To run your app on Android:
cd D:\WWW\567\a567
Have an Android emulator running (quickest way to get started), or a device connected
react-native run-android

yarn add react-native-gesture-handler
react-native link react-native-gesture-handler
```

## dva

[官方文档](https://dvajs.com/)

```bash
yarn global add dva-cli
dva new dva-quickstart
cd dva-quickstart
npm start
```

## umi

[官方文档](https://umijs.org/zh/)

```bash
yarn global add umi
mkdir myapp && cd myapp
yarn create umi
```

## react-native-ui-lib

[官方文档](http://wix.github.io/react-native-ui-lib/docs/Button/)

```js
const FLEX_KEY_PATTERN = /^flex(G|S)?(-\d*)?$/;
const PADDING_KEY_PATTERN = new RegExp(`padding[LTRBHV]?-([0-9]*|${Spacings.getKeysPattern()})`);
const MARGIN_KEY_PATTERN = new RegExp(`margin[LTRBHV]?-([0-9]*|${Spacings.getKeysPattern()})`);
const ALIGNMENT_KEY_PATTERN = /(left|top|right|bottom|center|centerV|centerH|spread)/;
```

## react-devtools

```bash
yarn global add react-devtools
react-devtools
```

## expo

[官方文档](https://docs.expo.io/versions/latest/workflow/expo-cli/)

```bash
https://github.com/mcnamee/react-native-starter-kit.git
yarn global add expo-cli
expo init expo-demo
cd expo-demo
expo start
expo build:android
expo build:status
expo doctor
```

## Ignite

[官方文档](https://infinite.red/ignite/)

```bash
yarn global add ignite-cli
ignite new PizzaApp
  ( Choose Andross when prompted )
cd PizzaApp
ignite add maps
ignite add vector-icons
ignite generate screen PizzaLocationList
ignite generate component PizzaLocation
ignite generate map StoreLocator
ignite add i18n
ignite remove i18n
ignite --help
```

## gatsby

[官方文档](https://www.gatsbyjs.org/)

```bash
yarn global add gatsby-cli
gatsby new gatsby-site
cd gatsby-site
yarn run develop
```

## taro

[官方文档](https://nervjs.github.io/taro/docs/GETTING-STARTED.html)

```bash
yarn global add @tarojs/cli
taro init ..
react-devtools
react-native run-android
```