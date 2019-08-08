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

## Weex

[官方文档](http://weex.apache.org/cn/guide/index.html)

```bash
npm install weex-toolkit -g
weex create awesome-app
cd awesome-app
npm install
npm start
weex platform add ios
weex platform add android
weex run ios
weex run android
weex run web
weex debug
```
