# Vue

[官方文档](https://cn.vuejs.org/)

Vue (读音 /vjuː/，类似于 view) 是一套用于构建用户界面的渐进式框架。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。Vue 的核心库只关注视图层，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与现代化的工具链以及各种支持类库结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。

## Vue CLI

[Vue-Cli3 官方文档](https://cli.vuejs.org/zh/guide/installation.html)
[Vue 的生命周期](https://cn.vuejs.org/v2/guide/instance.html#生命周期图示)

Vue 是一套用于构建用户界面的渐进式框架。

> **关于旧版本**
Vue CLI 的包名称由 vue-cli 改成了 @vue/cli。 如果你已经全局安装了旧版本的 vue-cli (1.x 或 2.x)，你需要先通过 `npm uninstall vue-cli -g` 或 `yarn global remove vue-cli` 卸载它。

```bash
yarn global add @vue/cli
vue --version
vue ui
vue create hello-world
vue add @vue/eslint
yarn serve
```

## Vue Router

[官方文档](https://router.vuejs.org/zh/)

Vue Router 是 Vue.js 官方的路由管理器。

## Vuex

[官方文档](https://vuex.vuejs.org/zh/)

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。

## Nuxt

[官方文档](https://zh.nuxtjs.org/guide)

Nuxt.js 是一个基于 Vue.js 的通用应用框架。通过对客户端/服务端基础架构的抽象组织，Nuxt.js 主要关注的是应用的 UI渲染。

```bash
yarn global add create-nuxt-app
create-nuxt-app ..
npm run dev
npm run generate
```

## Vuepress

[官方文档](https://www.vuepress.cn/)

Vue 驱动的静态站点生成工具

```bash
yarn global add vuepress
vuepress dev
vuepress build
```

##  Vue DevTools

- [Chrome 应用商店](https://chrome.google.com/webstore/detail/vuejs-devtools/nhdogjmejiglipccpnnnanhbledajbpd?utm_source=chrome-ntp-icon)
- 局域网镜像`\\192.168.1.100\nas\crx`


## Vue 端口映射

```bash
build/webpack.dev.conf.js
```
```js
  devServer: {
    disableHostCheck: true
  },
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

