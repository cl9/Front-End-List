# React
+ [React组件](#React组件)
  + [组件定义](#组件定义)
  + [组件生命周期](#组件生命周期)
  + [组件间通信](#组件间通信)
    + [父子组件间通信](#父子组件间通信)
  + [更新组件UI](#更新组件UI)
    + [不可变的State](#不可变的State)
  + [组件事件处理](#组件事件处理)
    + [事件语法](#事件语法)
    + [阻止事件默认行为](#阻止事件默认行为)

## React组件

### 组件定义

1. 函数组件
```
function Title(props) {
  return <h1>{props.name}</h1>;
}
```
2. class组件
```
class Title extends React.Component {
  render() {
    return <h1>{this.props.name}</h1>;
  }
}
```

### 组件生命周期
[生命周期图谱](http://projects.wojtekmaj.pl/react-lifecycle-methods-diagram/)

#### constructor()
1. 如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数
2. 要避免在构造函数中引入任何副作用或订阅
3. **避免将 props 的值复制给 state！这是一个常见的错误**

#### componentDidMount()
会在组件挂载后（插入 DOM 树中）立即调用。依赖于 DOM 节点的初始化应该放在这里。
1. 网络请求获取数据
2. 添加订阅
3. 创建 timer

#### componentDidUpdate(prevProps, prevState, snapshot)
1. 首次渲染不会执行此方法
2. 当组件更新后，可以在此处对 `DOM` 进行操作

#### componentWillUnmount()
会在组件卸载及销毁之前直接调用
1. 清除 timer
2. 取消网络请求
3. 清除订阅


### 组件间通信

#### 父子组件间通信
通过 `props` 属性传递

```
class Parent extends React.Component {
  render() {
    return <h1>{this.props.name}</h1>
  }
}

class Child extends React.Component {
  render() {
    return (
      <div>
        <Parent name = "React父子组件间通信" />
        <p>通过props属性传递</p>
      </div>
    );
  }
}
```

### 更新组件UI
通过 `state` 属性和 `setState` 方法

> <strong>注意: 不能直接修改state，组件并不会重新渲染组件</strong>,例如:
> <del>this.state.name = 'john'</del>是错误的,正确的方式应该是
>```
> this.setState({
>     name : 'john'  
> })
>```


`setState()` 可以接收一个对象或一个函数

1.  `state` 修改不依赖 `this.state` 的值,可以让 `setState()` 接收一个对象
```
this.setState({
    name : 'john'  
})
```
2. **因为 this.props 和 this.state 可能会异步更新，所以你不要依赖他们的值来更新下一个状态。** 要解决这个问题，可以让 setState() 接收一个函数而不是一个对象。
```
this.setState((state, props) => ({
  counter: state.counter + props.increment
}));
```

#### 不可变的State
React官方建议把State当作是不可变对象

##### 1. 状态的类型是不可变类型（数字，字符串，布尔值，null， undefined）
直接赋值

##### 2. 状态的类型是数组
1. 增: `concat` 或 `...` 扩展运算符替代 `push`、`unshift`
```
this.setState({
  titles: this.titles.concat(['React'])
})
或者
this.setState(preState => ({
  titles: [...preState.titles, 'React']
}))
```
2. 删: `slice` 替代 `pop`、`shift`、`splice`
```
this.setState({
  titles: this.titles.slice(0,2)
})
```
3. 改
```
var titles = this.state.titles;
titles[0] = 'Kotlin'
this.setState({
  titles: titles
})
```
4. 其他:过滤
```
this.setState({
  titles: this.titles.filter(title => {
    return title != 'React';
  });
})
```


##### 3. 状态的类型是普通对象（不包含字符串、数组）
1. 使用ES6 的Object.assgin方法
```
this.setState({
  person: Object.assign({}, person, {name: 'John'});
})
```
2. 使用`...` 扩展运算符
```
this.setState({
  person: {...person, name: 'John'};
})
```


### 组件事件处理

#### 事件语法

1. React 事件的命名采用小驼峰式（camelCase），而不是纯小写。
2. 使用 JSX 语法时你需要传入一个函数作为事件处理函数，而不是一个字符串。

HTML
```
<button onclick="activateLasers()"/>
```

React
```
<button onClick={activateLasers}/>
```

> 如果使用的 `class` 定义的组件,需要注意 `class` 的方法默认不会绑定 `this`,如何解决此问题:
> 1. 在构造函数中为该方法绑定this
> ```
> class Parent extends React.Component {
>   constructor(props){
>       super(props);
>       this.state = { name : '' }
>       // 为了在回调中使用 `this`，这个绑定是必不可少的
>       this.activateLasers = this.activateLasers.bind(this)
>   }  
>   activateLasers(){
>     this.setState(state => ({
>      name: 'john'
>     }));
>   }
>   render() {
>      return (
>       <div>
>         <button onClick={this.activateLasers} />
>         <p>{this.name}</p>
>       </div>
>      );
>   }
> }
> ```
> 2. 在回调中使用箭头函数
> ```
>  render() {
>    // 此语法确保 `handleClick` 内的 `this` 已被绑定。
>    return (
>      <button onClick={(e) => this.activateLasers(e)} />
>    );
>  }
> ```

#### 阻止事件默认行为

在 `React` 中另一个不同点是你不能通过返回 `false` 的方式阻止默认行为。你必须显式的使用 `preventDefault` 。
