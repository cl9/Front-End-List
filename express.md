+ [环境搭建](#环境搭建)
  1. [安装Node和NPM](##安装Node和NPM)
  2. [安装Express应用生成器](#安装Express应用生成器)
+ [创建项目](#创建项目)
+ [运行项目](#运行项目)


# 环境搭建

## 安装Node和NPM
## 安装Express应用生成器
可以生成一个 Express 应用的“框架”

安装:
```
npm install express-generator -g
```

# 创建项目
```
$ express --help

  用法：express [选项] [目录]

  选项：

        --version        打印版本号
    -e, --ejs            添加 ejs 引擎支持
        --pug            添加 pug 引擎支持
        --hbs            添加 handlebars 引擎支持
    -H, --hogan          添加 hogan.js 引擎支持
    -v, --view <engine>  添加 <engine> 试图引擎支持 (ejs|hbs|hjs|jade|pug|twig|vash) (默认为 jade)
    -c, --css <engine>   添加 <engine> 样式表引擎支持 (less|stylus|compass|sass) (默认为纯 css)
        --git            添加 .gitignore
    -f, --force          对非空文件夹强制执行
    -h, --help           打印帮助信息
```

例如:
```
$ express helloworld --git
```

# 运行项目
```
$ DEBUG=node-01:DEBUG=node-01:* npm start
```

## 文件改动时重启服务器
1. 在项目中安装 `nodemon`
```
npm install --save-dev nodemon
```
2. 找到 `package.json` 的 `scripts` 部分,在新的一行中添加 `"devstart"`
```
"scripts": {
    "start": "node ./bin/www",
    "devstart": "nodemon ./bin/www"
  },
```
3. 用新建的 `devstart` 命令启动服务器
```
$ DEBUG=express-locallibrary-tutorial:* npm run devstart
```


# 基于 express 的 RESTful 

## GET
```
router.get('/', function(req, res, next) {
  res.send('hello express restful!');
});
```

## POST
```
router.post('/', (req,res) => {
   res.end(JSON.stringify({
     smsCode : getRandomCode(),
     token : '短信模版'
   }))
})
```

# 使用 [express-validator](https://express-validator.github.io/docs/) 验证请求数据

## 基础验证
1. check([field, message]) 校验请求数据的字段
   > 校验的字段 `field` 可能来源于: 
   > * req.body —— body([fields, message]) (只校验req.body)
   > * req.cookies —— cookie([fields, message]) (只校验req.cookies)
   > * req.headers —— header([fields, message]) (只校验req.headers)
   > * req.params —— param([fields, message]) (只校验req.params)
   > * req.query —— query([fields, message]) (只校验req.query)
```
check('phone').isMobilePhone().withMessage('手机格式不正确')
```
2. validationResult(req) 获取请求数据校验的结果
```
var errors = validationResult(req);
   if(!errors.isEmpty()){
     res.json(errors.mapped());
     return;
}
```

**完整例子 —— 短信验证码接口:**
```
router.post('/', [
  check('phone').isLength(13).withMessage('手机号位数不够'),
  check('phone').isMobilePhone().withMessage('手机格式不正确')
 ], function(req,res,next){
   var errors = validationResult(req);
   if(!errors.isEmpty()){
     res.json(errors.mapped());
     return;
   }
   res.end(JSON.stringify({
     smsCode : getRandomCode(),
     token : '短信模版'
   }))
})
```

