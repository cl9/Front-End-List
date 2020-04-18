# 注册跳转设置密码
1. [跳转设置密码](#跳转设置密码)
    + [如何使用react-router](#如何使用?)
    + [BrowserRouter和HashRouter的区别](#BrowserRouter和HashRouter的区别)
    + [Switch和Route的区别](#Switch和Route的区别)
2. [将手机号传至设置密码(路由传参)](#将手机号传至设置密码)
    * [通过url拼接参数`?`](#通过url拼接参数`?`)
    * [路由表中通过`:`](#路由表中通过`:`)
    * [query](#query)
    * [state](#state)
    * [四种方式的对比](#四种方式的对比)

## 准备工作 —— 熟悉[React-Router](https://reacttraining.com/react-router/web/guides/quick-start)
* [React Router 中文文档（一）](https://segmentfault.com/a/1190000014294604)
* [初探 React Router 4.0](https://www.jianshu.com/p/e3adc9b5f75c/)

### 为什么要用react-router?
React Router 知道如何为我们搭建嵌套的 UI，因此我们不用手动找出需要渲染哪些组件。

### 如何使用?
[react-router和react-router-dom有什么区别](https://github.com/ReactTraining/react-router/issues/4648)
1. React Native app
    * NPM
    ```
    npm install --save react-router-native
    ```
2. React Web app
    * NPM
    ```
    npm install --save react-router-dom
    ```
    * UMD
    ```
    <script src="https://unpkg.com/react-router-dom/umd/react-router-dom.min.js"></script>
    ```

### BrowserRouter和HashRouter的区别
||BrowserRouter|HashRouter|
|:---:|:---:|:---:|
|实现|使用HTML5的[History](https://developer.mozilla.org/en-US/docs/Web/API/History)|使用window.location.hash|
|url表示|http://localhost:3000/react_router/index?id=2|http://localhost:3000/react_router/#index?id=2|
|传参(路由页面页面刷新数据不丢失)|url传值，路由参数传值，以及state|url传值，路由参数传值|
||推荐使用|不支持location.key 、location.state,仅用于支持旧版浏览器|

### Switch和Route的区别
需要做唯一匹配,即想要在众多路由中只匹配其中一个路由,则要用到`Switch`

## 跳转设置密码
1. 在`src`根目录下创建`routes.js`,创建路由数组包括每个页面的路由
```
import register from './pages/register';
import setPwd from './pages/setPwd';

const routes = [
  {
    path : '/',
    component: register,
    exact : true
  },
  {
    path : '/setpwd',
    component : setPwd
  }
]

export default routes
```
2. 在`App.js`入口文件中生成静态的路由
   * [BrowserRouter](https://reacttraining.com/react-router/web/api/BrowserRouter)
   * [Switch](https://reacttraining.com/react-router/web/api/Switch)
   * [Route](https://reacttraining.com/react-router/web/api/Route)
```
<BrowserRouter basename={baseurl}>
    <Switch>
      {routes.map((route,index) => {
        return <Route path={route.path} component={route.component} exact={route.exact} key={index}></Route>
        })}
    </Switch>
</BrowserRouter>
```

## 将手机号传至设置密码
路由传参有以下几种方法:
* 通过url拼接参数`?`
* 路由表中通过`:`
* query
* state

### 通过url拼接参数`?`
#### 传参
```
this.props.history.push('/setpwd?phone=18909090909')
```
#### 取参
<br/>通过[qs](https://github.com/ljharb/qs)库
```
import Qs from 'qs';

const queryString = Qs.parse(this.props.location.search,{ignoreQueryPrefix: true});
    const {phone = ''} = queryString 
```

### 路由表中通过`:`
#### 传参
1. 修改路由表中对应的路由
```
{
  path : '/setpwd/:phone',
  component : setPwd
}
```
2. 传参
```
this.props.history.push('/setpwd/18909090909')
```

#### 取参
```
const {phone = ''} = this.props.match.params
```

### query
#### 传参
```
const path = {
      pathname : '/setpwd',
      query : {
        phone : '18909090909'
      }
    }
this.props.history.push(path)
```

#### 取参
```
const {phone = ''} = this.props.location.query;
```

### state
#### 传参
```
this.props.history.push('/setpwd',{
      phone : '18909090909'
})
```

#### 取参
```
const {phone = ''} = this.props.location.state;
```

### 四种方式的对比
||?拼接参数|:id|state|query|
|:---:|:---:|:---:|:---:|:---:|
|优点|路由页面页面刷新数据不丢失|路由页面页面刷新数据不丢失|参数不暴露在url上|参数不暴露在url上|
|缺点|1. 取参比较麻烦 2. 参数直接暴露在url|1. 增加参数比较麻烦 2. 参数直接暴露在url|路由页面页面刷新,BorwserRouter数据不丢失|路由页面页面刷新数据丢失,HashRouter数据会丢失|

# 设置密码
