- [开发前的准备工作](#开发前的准备工作)
  - [推荐安装VsCode](#推荐安装VsCode)
  - [VsCode调试](#VsCode调试)
  - [自动重启nodemon](#自动重启nodemon)
  - [nodemon+VsCode调试](#nodemon+VsCode调试)

- [koa中间件](#koa中间件)
  - [路由 koa-router](#路由koa-router)
  - [路由动态注册require-directory](#路由动态注册require-directory)
  - [全局异常](#全局异常)
  - [数据库ORM框架Sequelize](#数据库ORM框架Sequelize)


# 开发前的准备工作

## 推荐安装VsCode

## VsCode调试

1. 点击左侧面板的![调试](https://pics1.baidu.com/feed/a1ec08fa513d2697075ec011bb895bff4216d861.jpeg?token=84376b39dc37f26bad6310411a001fdc&s=E9C233674EEC19325AFDB50B0000A091)
2. 选择 Debug> Add configurations 菜单命令
3. 在弹出的 launch.json 文件中可以修改调试配置，例如

```
"configurations": [
    {
      "type": "node",
      "request": "launch",
      "name": "调试当前打开的文件",
      "program": "${file}"
    }

    {
      "type": "node",
      "request": "launch",
      "name": "调试node项目",
      "program": "${workspaceFolder}\\app.js"
    }
  ]
```

## 自动重启nodemon

> **背景**: 安装 nodemon 之前，每次修改完 nodejs 代码，都需要`node xxx.js`命令重启服务，安装 nodemon 之后，每次修改完代码保存后将自动重启服务，简化操作

1. 全局安装 nodemon(nodemon 仅用于测试环境)

```
npm i nodemon -g
```

2. 使用 nodemon 替代 node 启动服务

```
nodemon xxx.js
```

## nodemon+VsCode调试

在弹出的 launch.json 文件中添加 nodemon 配置，

```
    {
      "type": "node",
      "request": "launch",
      "name": "nodemon",
      "runtimeExecutable": "nodemon",
      "program": "${workspaceFolder}/app.js",
      "restart": true,
      "console": "integratedTerminal",
      "internalConsoleOptions": "neverOpen"
    }
```

# koa中间件

![洋葱模型](https://upload-images.jianshu.io/upload_images/15401334-252759789ba9be10.png?imageMogr2/auto-orient/strip|imageView2/2/format/webp)

## 路由koa-router

> **背景**：安装 koa-router 之前，多个 api 可能如下编写
>
> ```
> app.use(async (ctx, next) => {
>   if (ctx.path === "/book") {
>     ctx.body = "<p>一本书</p>";
>   } else if (ctx.path === "/music") {
>     ctx.body = "<p>一首歌</p>";
>   }
> });
> ```
>
> 安装 koa-router 之后，可以通过中间件简化 if 判断

1. 安装 koa-router

```
npm i koa-router
```

2. 引入 koa-router

```
const Router = require('koa-router')
```

3. 实例化

```
var router = new Router()
```

4. 调用 koa-router 的 Rest 方法，例如 get、post、pull、delete 等

```
router.get("/", (ctx, next) => {
  ctx.body = "<span>哼哼哈哈</span>";
});
```

5. 注册中间件

```
app.use(router.routes())
```

## 路由动态注册require-directory

> **背景**：安装 require-directory 之前，路由都在 app.js 中注册，例如:
>
> ```
> router.get("/book", (ctx, next) => {
>
> });
>
> router.get("/music", (ctx, next) => {
>
> });
> ```
>
> 安装 require-directory 之后，路由可以动态注册

1. 安装 require-directory

```
npm i require-directory
```

2. 新建目录存放 api，例如`/app/api/v1/book.js`或`/app/api/v1/music.js`
3. 使用 require-directory 动态注册`/app/api/v1`目录下的路由,通过 node 的`process.cwd()`方法获得根目录

```
requireDirectory(module, `${process.cwd()}/app/api/v1`, {
      visit: obj => {
        if (obj instanceof Router) {
          app.use(obj.routes());
        }
      }
});
```

## 全局异常

### 已知异常

### 未知异常

## 数据库ORM框架Sequelize
> Sequelize 是一款基于 Nodejs 功能强大的异步 ORM 框架。
同时支持 PostgreSQL, MySQL, SQLite and MSSQL 多种数据库，很适合作为 Nodejs 后端数据库的存储接口，为快速开发 Nodejs 应用奠定扎实、安全的基础。

**注意：本文基于MySQL数据库**

### xampp 安装使用

[xampp 安装](https://blog.csdn.net/qq_36595013/article/details/80373597)

### xampp 修改数据库 root 用户的密码

> 如果通过 UPDATE 直接编辑 user 表`update user set password=password('123') where user='root'`修改 root 默认密码会提示<strike>`Column 'Password' is not updatable`</strike>

mariadb 从版本 10.4 开始，将自动安全地创建 root 帐户，因此安装不需要密码。

1. 点击 XAMPP Control 面板运行 Apache 和 MySQL，点击 shell 进入命令行
2. 连接数据库 `# mysql -u root`
3. 可以在 root 用户访问后使用 SET 命令轻松更改此设置

```
MariaDB [(none)]> set password = password('123')
```

### Navicat 连接数据库

> 注意：Navicat 点击用户出现<strike>`1054 Unknown column 'password_lifetime' in 'field list'`</strike>，不要使用 MySQL 连接数据库，使用 MariaDB

### 使用 Sequelize 操作数据库

1. 安装 Sequelize 和数据库驱动(例如：mysql2)

```
npm i sequelize
npm i mysql2
```

2. 建立连接

```
var db = new Sequelize('database', 'username', 'password', {
  host: 'localhost',
  dialect: 'mysql'|'mariadb'|'sqlite'|'postgres'|'mssql',

  pool: {
    max: 5,
    min: 0,
    idle: 10000
  },

  // 仅 SQLite 适用
  storage: 'path/to/database.sqlite'
});
```

3. 新建模型，例如用户 model

```
class User extends Model {}

User.init(
  {
    id: {
      type: Sequelize.INTEGER,
      primaryKey: true,
      autoIncrement: true
    },
    nickname: Sequelize.STRING,
    email: Sequelize.STRING,
    password: Sequelize.STRING,
  },
  {
    sequelize: db,
    tableName: "user"
  }
);
```

4. 模型与数据库同步,执行下列方法就可以在数据库中创建对应的表结构

```
db.sync()
```
