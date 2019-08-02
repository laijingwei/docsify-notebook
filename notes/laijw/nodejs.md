# Node.js

## MongoDB

> [官方文档](https://docs.mongodb.com/manual/reference/program/mongoexport/)

- 安装路径

`C:\Program Files\MongoDB\Server\4.0\bin`

- 启动 shell

```bash
mongo
```

- 新建视图

```bash
db.createView("man","users",{$match:{sex:1}})
```

- 导入

```bash
mongoimport --db users --collection contacts --file contacts.json --jsonArray
```

- 导出

```bash
mongoexport --db users --collection contacts --out contacts-out.json --jsonArray --pretty
```

- 备份

```bash
mongodump -h localhost -d users -o .
```

- 恢复

```bash
mongorestore -h localhost -d users .
```


## adminMongo

> MongoDB Web 可视化工具

```bash
git clone https://github.com/mrvautin/adminMongo
cd adminMongo
npm install
npm start
http://127.0.0.1:1234 
mongodb://127.0.0.1:27017
```

## nodemon

> node.js 版本的 live-server

```bash
yarn global add nodemon
nodemon -h
nodemon ./server.js localhost 8080
```

## pm2

> node.js 进程管理器

```bash
# 查看端口占用情况
netstat -ano
yarn global add pm2

# 启动 nodejs 服务器
pm2 start app.js --name .. --watch

# 启动静态文件服务器
pm2 serve . 9003 --spa --name hugo-blog --watch

# 启动 Vue 项目
pm2 start npm --name 805-aap -- run dev

# 查看pm2管理的应用运行状态
pm2 ls

# pm2 停止进程
pm2 stop ..
pm2 delete ..

# 开机自动启动已启动的服务
pm2 start ..
pm2 save
pm2 startup

# 删除自动启动服务
pm2 unstartup systemd
```

## hotel

> node.js 端口管理器

```bash
yarn global add hotel && hotel start

http://localhost:2000/

# Use

hotel add <cmd|url> [opts]
hotel run <cmd> [opts]

# Examples

hotel add 'nodemon app.js' --out dev.log  # Set output file (default: none)
hotel add 'nodemon app.js' --name name    # Set custom name (default: current dir name)
hotel add 'nodemon app.js' --port 3000    # Set a fixed port (default: random port)
hotel add 'nodemon app.js' --env PATH     # Store PATH environment variable in server config
hotel add http://192.168.1.10 --name app  # map local domain to URL

hotel run 'nodemon app.js'                # Run server and get a temporary local domain

# Other commands

hotel ls     # List servers
hotel rm     # Remove server
hotel start  # Start hotel daemon
hotel stop   # Stop hotel daemon
```

## json server

> 接口本地测试服务器

```json
{
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

```bash
yarn global add json-server
json-server --watch db.json --port 3000
json-server index.js
http://localhost:3000/posts/1

GET    /posts
GET    /posts/1
POST   /posts
PUT    /posts/1
PATCH  /posts/1
DELETE /posts/1
```

## Mock.js

[官方文档](http://mockjs.com/examples.html)

> 模拟数据工具 

```js
id: i,
user_id: Random.id(),
detail: Random.csentence(5, 30),
thumb: Random.dataImage('64x64', 'mock'),
email: Random.email(),
address: Random.county(true),
title: Random.cword(8,20),
city: Random.city(),
name: Random.cname(),
date: Random.date(),
desc: content.substr(0,40),
tag: Random.cword(2,6),
views: Random.integer(100,5000),
images: images.slice(0,Random.integer(1,3))
```

## composer

> PHP 包管理器

```bash
# composer 中国镜像
composer config -gl
composer config -g repo.packagist composer https://packagist.phpcomposer.com
composer require ..
```

## lumen

> 基于 Laravel 的轻量框架

```bash
composer global require "laravel/lumen-installer"
lumen new blog
php -S localhost:8000 -t public
```

## laravel

> PHP MVC 框架

```bash
composer global require laravel/installer
laravel new blog
php artisan serve
php artisan list
php artisan make:controller API/PhotoController --api --model=Models/Photo
php artisan make:migration create_photos_table
php artisan migrate
php artisan make:seeder PhotosTableSeeder
php artisan db:seed

Route::namespace('API')->group(function () {
    Route::apiResource('photos', 'PhotoController');
});

http://127.0.0.1:8000/api/photos
```

> Actions Handled By Resource Controller

| Verb      | URI             | Action  | Route Name     |
| --------- | --------------- | ------- | -------------- |
| GET       | /photos         | index   | photos.index   |
| POST      | /photos         | store   | photos.store   |
| GET       | /photos/{photo} | show    | photos.show    |
| PUT/PATCH | /photos/{photo} | update  | photos.update  |
| DELETE    | /photos/{photo} | destroy | photos.destroy |

## adonis

> 类 laravel 的 node.js 框架

```bash
yarn global add adonis-cli
adonis new blog
cd blog
npm run serve:dev
node ace
node ace make:controller User --resource
node ace make:model User
node ace make:migration users --create=users
node ace migration:run
node ace migration:status
node ace make:seed User
```

## fastify-cli

> node.js 高性能框架

```bash
# 全局安装
yarn global add fastify-cli
fastify generate

# 项目引入
yarn add fastify
```

```js
// Require the framework and instantiate it
const fastify = require('fastify')({
  logger: true
})
 
// Declare a route
fastify.get('/', (request, reply) => {
  reply.send({ hello: 'world' })
})
 
// Run the server!
fastify.listen(3000, (err, address) => {
  if (err) throw err
  fastify.log.info(`server listening on ${address}`)
})
```

## sails

> 类 ruby on rails 的 node.js 框架

```bash
yarn global add sails
sails new sails-api --no-front-end --fast
cd sails-api
sails generate api test
sails lift
```

To use MongoDB in your Node.js/Sails app during development:

1.  Run `npm install sails-mongo` in your app folder.
2.  In your `config/datastores.js` file, edit the `default` datastore configuration:

    ```
    default: {
       adapter: 'sails-mongo',
       url: 'mongodb://root@localhost/foo'
     }

    ```

3.  In your `config/models.js` file, edit the default `id` attribute to have the appropriate `type` and `columnName` for MongoDB's primary keys:

    ```
    attributes: {
       id: { type: 'string', columnName: '_id' },
       //...
     }

    ```

That's it! Lift your app again and you should be good to go.


| Route                                                             | Blueprint Action                                                                | Example URL                                              |
| ----------------------------------------------------------------- | ------------------------------------------------------------------------------- | -------------------------------------------------------- |
| GET /:modelIdentity/find                                          | [find](https://sailsjs.com/documentation/reference/blueprint-api/find-where)    | `http://localhost:1337/user/find?name=bob`               |
| GET /:modelIdentity/find/:id                                      | [findOne](https://sailsjs.com/documentation/reference/blueprint-api/find-one)   | `http://localhost:1337/user/find/123`                    |
| GET /:modelIdentity/create                                        | [create](https://sailsjs.com/documentation/reference/blueprint-api/create)      | `http://localhost:1337/user/create?name=bob&age=18`      |
| GET /:modelIdentity/update/:id                                    | [update](https://sailsjs.com/documentation/reference/blueprint-api/update)      | `http://localhost:1337/user/update/123?name=joe`         |
| GET /:modelIdentity/destroy/:id                                   | [destroy](https://sailsjs.com/documentation/reference/blueprint-api/destroy)    | `http://localhost:1337/user/destroy/123`                 |
| GET /:modelIdentity/:id/:association/add/:fk                      | [add](https://sailsjs.com/documentation/reference/blueprint-api/add-to)         | `http://localhost:1337/user/123/pets/add/3`              |
| GET /:modelIdentity/:id/:association/remove/:fk                   | [remove](https://sailsjs.com/documentation/reference/blueprint-api/remove-from) | `http://localhost:1337/user/123/pets/remove/3`           |
| GET /:modelIdentity/:id/:association/replace?association=[1,2...] | [replace](https://sailsjs.com/documentation/reference/blueprint-api/replace)    | `http://localhost:1337/user/123/pets/replace?pets=[3,4]` |