# NPM 常用库集合

## NPM

[npm 中文文档](https://www.npmjs.cn/)

```bash
# npm 中国镜像
npm config get registry
npm config set registry https://registry.npm.taobao.org
npm config set disturl https://npm.taobao.org/dist

# 查看本机 npm 全局安装列表
npm list -g --depth 0

npm install -g jshint
npm uninstall -g jshint
npm update -g jshint
```

## Yarn

[yarn 中文文档](https://yarn.bootcss.com/)

```bash
npm install -g yarn

# yarn 中国镜像
yarn config get registry
yarn config set registry https://registry.npm.taobao.org
yarn config set disturl https://npm.taobao.org/dist

yarn add ..
yarn add .. -D
yarn global add ..
yarn global list
yarn config list
yarn remove ..
yarn upgrade
```


## Live-Server

> Node.js 服务器

```bash
yarn global add live-server
live-server
--port=NUMBER - select port to use, default: PORT env var or 8080
--host=ADDRESS - select host address to bind to, default: IP env var or 0.0.0.0 ("any address")
--no-browser - suppress automatic web browser launching
--browser=BROWSER - specify browser to use instead of system default
```

## Hexo

> 静态博客生成器

```bash
yarn global add hexo-cli
yarn add hexo-neat --save
hexo init blog
hexo new "Hello Hexo"
hexo new page "about"
hexo server
hexo generate

# hexo-next
```bash
cd your-hexo-site
git clone https://github.com/iissnan/hexo-theme-next themes/next
#about: /about
```

## Docsify

[官方文档](https://docsify.js.org/#/zh-cn/)

> 文档生成器

```bash
yarn global add docsify-cli
docsify init ..
docsify serve
```

## dlf

> node_modules 快速删除

```bash
yarn global add dlf
dlf file
dlf directory
```

## rimraf

> The UNIX command rm -rf for node

```bash
yarn global add rimraf
rimraf file
rimraf directory
```

## Bower

> 静态库包管理器

```bash
yarn global add bower
bower -h
bower init
bower install jquery --save
bower info jquery
bower search bootstrap
bower uninstall jquery
```

## Angular-CLI

[中文文档](https://www.angular.cn/)

```bash
yarn global add @angular/cli
ng new my-app
cd my-app
ng serve --open
```

## Ionic

[官方文档](https://ionicframework.com/docs)

```bash
yarn global add ionic cordova
ionic start helloWorld blank
cd helloWorld
ionic serve
```