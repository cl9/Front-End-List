# 原型设计
参考

* [Mockplus](https://www.mockplus.cn/sample/tags?name=App原型设计)

# UI设计
参考

* [千图网](https://www.58pic.com)
* [站酷](https://www.zcool.com.cn/discover/17!3!0!0!0!!!!2!-1!1)


# 项目代码编写

## 项目创建

### 使用 `React` 脚手架 `create-react-app `
1. 安装
```
npm install -g create-react-app
```
2. 创建
```
create-react-app zero-foods
```
3. 运行
```
npm start
```
+ npm run start : 开始项目，通过http://localhost:3000 可访问项目；
+ npm run build : 项目打包，在生产环境中编译代码，并放在build目录中；所有代码将被正确打包，并进行优化、压缩同时使用hash重命名文件；执行该命令前需要在package.json中新增条配置"homepage": "."（上面配置文件已给出）, 同时build后的项目需要在服务器下才能访问；否则打开的将是空白页面；
+ npm run test : 交互监视模式下启动测试运行程序；
+ npm run eject : 将隐藏的配置导出；需要知道的是create-react-app脚手架本质上是使用react-scripts进行配置项目，所有配置文件信息都被隐藏起来(node_modules/react-scripts)；当需要手动修改扩展webpack配置时有时就需要将隐藏的配置暴露出来；特别需要注意的是该操作是一个单向操作，一旦使用eject，那么就不能恢复了(再次将配置隐藏)；

### 项目目录结构
```
- zero-foods
    - dist // 存放编译后的文件

    - config
      - config.js  // 配置文件
    - mock
      - index.js   // 前端模拟请求数据

    - src  // 应用的所有代码
      - actions     // 处理异步请求
      - assets      // 静态资源
      - components  // 公用组件
      - pages       // 业务逻辑页面
      - reducers    // reducer 状态处理
      - util        // 公用方法
      - index.html  // 项目模板
      - index.js    // 项目入口
    - package.json      // npm init 自动生成
```

### 项目框架
+ [antd-mobile](https://mobile.ant.design/docs/react/introduce-cn)


#### antd
##### 在 create-react-app 中使用Antd
>参考[通过create-react-app从零搭建react环境](https://segmentfault.com/a/1190000015301231))

通过 babel-plugin-import + react-app-rewired实现按需加载（官网推荐）

1. react-app-rewired：主要用于在不暴露配置的情况下对webpack的配置进行扩展；
    + 安装依赖包 react-app-rewired：
    ```
    $ npm install react-app-rewired --save-dev
    ```
    + 修改 package.json 中的脚本命令：修改如下
    ```
    "scripts": {
    "start": "react-app-rewired start",
    "build": "react-app-rewired build",
    "test": "react-app-rewired test --env=jsdom",
    "eject": "react-app-rewired eject"
    }
    ```
    + 在项目根目录下(和 package.json 同级)新建配置文件 config-overrides.js ,**主要通过该配置文件修对webpack的配置进行修改**
2. babel-plugin-import 是一个用于按需加载组件代码和样式的 babel 插件
    + 安装依赖包：babel-plugin-import
    ```
    $ npm install babel-plugin-import --save-dev
    ```
    + 通过 react-app-rewired 对 webpack 配置进行扩展添加新的babel插件，config-overrides.js 修改 ( 添加 ) 如下内容：
    ```    
    // 引入 react-app-rewired 添加 babel 插件的函数
    const { injectBabelPlugin } = require('react-app-rewired');
    module.exports = function override(config,env) {
        config = injectBabelPlugin(['import',{ libraryName: 'antd-mobile',style:'css'}],config)
        return config
    }
    ```
    + 配置完后可直接导入 antd 的组件，不再需要另外引入css样式；
    ```   
    import { Button } from 'antd';
    ```

##### react-app-rewired问题集
1. `The "injectBabelPlugin" helper has been deprecated as of v2.0.`
需安装低版本
```
npm i react-app-rewired@2.0.2-next.0
```
2. `Cannot find module`
+ 删除 node_modules 文件夹
+ 重新 npm install

## 项目模块编写
1. 注册登录模块
2. 美食列表模块
3. 美食详情模块
4. 个人设置模块
5. 搜索模块

## 移动端适配
* 1px问题
* UI图完美适配方案
* iPhoneX适配方案
* 横屏适配
* 高清屏图片模糊问题

> 参考
> + [关于移动端适配，你必须要知道的](https://juejin.im/post/5cddf289f265da038f77696c)
> + [阿里最新的适配方案Fusion Design](https://fusion.design/design/doc/16)

### 通过vw/vh来实现自适应
css3中引入了一个新的单位vw/vh，与视图窗口有关。任意层级元素，在使用vw单位的情况下，1vw都等于视图宽度的百分之一。

#### 如何自动将px转化成vw —— [postcss-px-to-viewport](https://github.com/evrone/postcss-px-to-viewport) 插件

> 参考
> * [
create-react-app+react-app-rewired搭建viewport解决方案](https://segmentfault.com/a/1190000016780204)

`create-react-app`+`react-app-rewired`+`vw`
1. 安装
```
npm install postcss-px-to-viewport --save-dev
```
2. 配置config-overrides.js
```
module.exports = function override(config,env) {
    require('react-app-rewire-postcss')(config, {
      plugins: loader => [
          require('postcss-px-to-viewport')({
              viewportWidth: 750,      // 视窗的宽度，对应的是我们设计稿的宽度，一般是750
              viewportHeight: 1334,    // 视窗的高度，根据750设备的宽度来指定，一般指定1334，也可以不配置
              unitPrecision: 3,        // 指定`px`转换为视窗单位值的小数位数（很多时候无法整除）
              viewportUnit: 'vw',      // 指定需要转换成的视窗单位，建议使用vw
              selectorBlackList: ['.ignore', '.hairlines'],  // 指定不转换为视窗单位的类，可以自定义，可以无限添加,建议定义一至两个通用的类名
              minPixelValue: 1,       // 小于或等于`1px`不转换为视窗单位，你也可以设置为你想要的值
              mediaQuery: false       // 允许在媒体查询中转换`px`
          }),
      ]
    });
    return config;
}
```
3. **如何避免第三方库的px也被转换成vw了,例如antd?**
```
plugins: loader => [
    require('postcss-px-to-viewport')({
        ...
        exclude: [/node_modules/] // 新增exclude选项剔除第三方库
    }),
]
```