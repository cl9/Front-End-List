# React小技巧&第三方库
## 小技巧
* [HOC组件](https://react.docschina.org/docs/higher-order-components.html)
* [使用 PropTypes 进行类型检查](https://react.docschina.org/docs/typechecking-with-proptypes.html)

## 第三方库
* 样式
  * [在React项目中更好的使用className](#在React项目中更好的使用className)
  * [CSS预处理器](#CSS预处理器)
* UI组件库
  * [antd-mobile](#antd-mobile)
  * [React表单](#React表单)
# 样式
## 在React项目中更好的使用className
* [每日质量NPM包-classnames](https://www.cnblogs.com/soyxiaobi/p/9729289.html)
```
render() {
  let className = 'menu';
  if (this.props.isActive) {
      className += ' menu-active';
  }
  return <span className={className}>Menu</span>
}
```
**CSS 的 `class` 依赖组件的 `props` 或 `state`的情况很常见,如果你经常发现自己写类似这样的代码，[classnames](https://www.npmjs.com/package/classnames#usage-with-reactjs)以简化这一过程。**
```
const className = classnames({
      'menu': true,
      'menu-active': this.props.isActive 
})
```

## CSS预处理器
  * 使用 [SASS](https://www.sass.hk/),它在 CSS 语法的基础上增加了变量 (variables)、嵌套 (nested rules)、混合 (mixins)、导入 (inline imports) 等高级功能。

## UI组件库
* [antd-mobile](https://mobile.ant.design/docs/react/introduce-cn)

### React表单
官方推荐的解决方案:[Formik](https://jaredpalmer.com/formik)

#### antd-mobile与Formik结合使用
* [
Formik与antd-mobile的移动端的表单实践 (上) ](https://segmentfault.com/a/1190000016171909)
* [
Formik与antd-mobile的移动端的表单实践（下）](https://segmentfault.com/a/1190000016525510)

1. 安装Formik
```
npm install formik --save
```


# Mobx vs Redux

<table>
  <tr>
    <th></th>
    <th colspan="2">Mobx</th>
    <th>Redux</th>
  </tr>
  <tr>
    <td rowspan="7">State(状态)</td>
    <td colspan="2">
      <ul>
        <li><strong>使用observable(value)系列函数</strong>
          <pre>const list = observable([1, 2, 4])</pre></li>
        <li><strong>使用@observable 装饰器</strong>
          <pre>
class OrderLine {
    @observable price = 0;
    @observable amount = 1;
            
    @computed get total() {
        return this.price * this.amount;
    }
}
          </pre>
        </li>
      </ul>
    </td>
    <td>State</td>
  </tr>
  <tr>
    <td colspan="2">
      <ul>
        <li>State是可以修改的,可以定义任何数据结构</li>
        <li>任何可观察对象默认通过<code>observable</code>传递使其转变成可观察的,比如 <code>Observable Object</code> 的属性会默认转变成可观察的</li>
        <li>要禁止这种默认转换,可以传入<code>{ deep: false }</code></li>
      </ul>
    </td>
    <td>State是只读的</td>
  </tr>
  <tr>
    <td rowspan="2">Object</td>
    <td>普通对象(<strong>不是使用构造函数创建出来的对象,以 Object 作为其原型，或者根本没有原型</strong>)</td>
    <td></td>
  </tr>
  <tr>
    <td>非普通对象</td>
    <td></td>
  </tr>
  <tr>
    <td>Array</td>
    <td>
      <ul>
        <li>对于原生数组如何转换为可观察数组:
          <ul>
            <li><strong>observable.array</strong>
              <pre>
var todos = observable.array([
    { title: "Spoil tea", completed: true },
    { title: "Make coffee", completed: false }
]);
              </pre>
            </li>
            <li><strong>observable(array)</strong>
              <pre>
var todos = observable([
    { title: "Spoil tea", completed: true },
    { title: "Make coffee", completed: false }
]);                
              </pre>
            </li>
          </ul>
        </li>
        <li>对于可观察数组如何转换为原生数组
          <ul>
            <li><strong>slice</strong>
              <pre>
todos.slice()
              </pre>
            </li>
            <li><strong>Array.from</strong>
              <pre>
Array.from(todos)                
              </pre>
            </li>
          </ul>
        </li>
      </ul>
    </td>
  </tr>
  <tr>
    <td>Map</td>
    <td>
      <ul>
        <li><strong>observable.map(values)</strong></li>
        <li><strong>observable(new Map())</strong></li>
      </ul>
    </td>
    <td></td>
  </tr>
  <tr>
    <td>原始类型和引用类型</td>
    <td>
      <strong>observable.box(value)</strong>
    </td>
    <td></td>
  </tr>
</table> 