## 在线编译网站

+ [Kotlin在线编译](https://play.kotlinlang.org/)
+ [CodePen前端在线编码](https://codepen.io)

------

## 数据类型

<table>
    <tr>
        <th>数据类型</th>
        <th>Java</th>
        <th>ECMAScript</th>
        <th>Kotlin</th>
    </tr>
    <tr>
        <td rowspan="2">字符串</td>
        <td colspan="3">
            <ol>
                <li>
                    可以使用<code>+</code>拼接:
                    <code>val s = "abc"+1</code>
                </li>
                <li>转义字符使用传统的反斜杠方式</li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>1. 字符串是引用类型</td>
        <td>
            <table>
                <tr>
                    <th>ES5</th>
                    <th>ES6</th>
                </tr>
                <tr>
                    <td>
                        <ol>
                            <li>字符串字面量可以通过<code>\</code>拆分成多行
                            <pre>
"Hello\
,\
JavaScript
"
                            </pre>
                            </li>
                            <li>比较字符串只需要使用比较表达式(&lt;&gt;&lt;=&gt;)</li>
                        </ol>
                    </td>
                    <td>
                        <ol>
                            <li><strong>模版字符串<code>``</code></strong>
                                <ul>
                                    <li>结合html标签
                                        <pre>
`Hello <strong>Wolrd</strong>!`
                                        </pre>
                                    </li>
                                    <li>嵌入变量<code>${}</code>
                                        <pre>
`username is ${username}`                                        
                                        </pre>
                                    </li>
                                    <li>嵌入方法
                                        <pre>
function hello(){
    return 'Hello Wolrd!'
}           
console.log(`${hello()}`)                           
                                        </pre>
                                    </li>
                                </ul>
                            </li>
                            <li>ES6 为字符串添加了遍历器接口,使得字符串可以被for...of循环遍历。
                                最大的优点是可以识别大于0xFFFF的码点，传统的for循环无法识别这样的码点
                                <pre>
let text = String.fromCodePoint(0x20BB7);

for (let i = 0; i &lt; text.length; i++) {
    console.log(text[i])
}
  
// " "
// " "

for (let i of text) {
  console.log(i);
}
// "𠮷"                                    
                                </pre>
                            </li>
                        </ol>
                    </td>
                </tr>
            </table>
        </td>
        <td>
            <ol>
                <li>
                    保留原始字符串""":
                    <pre>
                    """
                    for(c in "foo") {
                        print (c)
                    }
                    """
                    </pre>
                </li>
                <li>字符串模版(<strong>Kotlin推荐的字符串拼接</strong>):
                    <pre>
                        val s = "Kotlin" 
                        print("$s.length is ${s.length}")
                    </pre>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>数字</td>
        <td>byte、short、int、long、float、double</td>
        <td>原始数据类型<code>number</code>:<code>3.14</code>,封装类型<code>Number</code>:<code>Number(3.14)</code>
            <ol>
                <li><strong>数字类型基于 IEEE 754 浮点数表示法,这是一种二进制表示法,二进制表示法并不能精确表示类似0.1这样简单的数字</strong>
                    <pre>
// 判断浮点数是否相等会出现问题
var x = .4 - .3
var y = .2 - .1
x == y // false
                    </pre>
                </li>
                <li><strong>它并没有为整数给出一种特定的类型</strong></li>
                <li><strong>严格模式下,数值常量字面值不支持八进制</strong></li>
                <li><strong>正无穷Infinity:超出<code>Number.MAX_VALUE</code>;负无穷-Infinity:超出<code>Number.MIN_VALUE</code></strong></li>
                <li><strong>NaN:非数值(Not a Number)是一个特殊的数值,任何数值除以 0 会返回 NaN</strong></li>
            </ol>
        </td>
        <td>
            <ol>
                <li>内置类型:Byte、Short、Int、Long、Float、Double</li>
                <li><strong>数值常量字面值不支持八进制</strong></li>
                <li>浮点数字面值默认double,float的表示方法和Java一致使用f或F:<code>123.2f</code></li>
                <li><strong>数字字面值可以使用下划线更易读:<code>100_000_000</code></strong></li>
                <li><strong>较小的类型不能隐式类型转换为较大的类型</strong></li>
            </ol>
        </td>
    </tr>
    <tr>
        <td rowspan="2">布尔</td>
        <td colspan="3">基础类型boolean,封装类型Boolean,字面值只有两个:true和false</td>
    </tr>
    <tr>
        <td>boolean</td>
        <td>
            <ol>
                <li><code>undefined、null、0、-0、NaN、""</code>会被转换成false</li>
                <li>所有其他值(包括所有对象、数组)都会转换成true</li>
            </ol>
        </td>
        <td><code>Boolean</code>类型:true或false</td>
    </tr>
    <tr>
        <td>字符</td>
        <td>char</td>
        <td>--</td>
        <td><code>Char</code>类型:<br />1. 不能直接当作数字<br />2. 可使用toInt()转换</td>
    </tr>
    <tr>
        <td>空</td>
        <td>--</td>
        <td><code>Null</code>:<strong>如果定义的变量准备在将来用于保存对象,有必要把一个变量的值显式地设置为 null</strong>
            <ol>
                <li>
                    <pre>
typeof(null) //返回object                        
                    </pre>
                </li>
                <li>
                    <pre>
null == undefined //返回 true
null === undefined //返回false                        
                    </pre>
                </li>
            </ol>
        </td>
        <td>--</td>
    </tr>
    <tr>
        <td>未定义</td>
        <td>--</td>
        <td><code>Undefined</code>:声明未定义的变量的初始值,<strong>没有必要把一个变量的值显式地设置为 undefined</strong>
            <pre>
var x;
typeof(x);  // undefined
            </pre>
        </td>
        <td>--</td>
    </tr>
    <tr>
        <td>代表</td>
        <td>--</td>
        <td>
            <table>
                <tr>
                    <th>ES5</th>
                    <th>ES6</th>
                </tr>
                <tr>
                    <td>--</td>
                    <td><code>Symbol</code>:一种实例是唯一且不可改变的数据类型
                        <ol>
                            <li>作为属性名
                                <pre>
let s = Symbol();
let obj = {
    &#91;s&#93;(args){
        return `Hello ${args}`
    }
}
console.log(obj[s]('JavaScript'))                                
                                </pre>
                            </li>
                            <li>作为常量
                                <pre>
const ACTION_DOWN = Symbol();
const ACTION_UP = Symbol();

getAction = (action) =>{
    switch(action){
        case ACTION_DOWN:
            console.log("手指按下");
            break;
        case ACTION_UP:
            console.log("手指抬起");
            break;
        default:
            console.log("初始");
            break;
    }
}
getAction(ACTION_DOWN);
                                </pre>
                            </li>
                        </ol>
                    </td>
                </tr>
            </table>
        </td>
        <td>--</td>
    </tr>
</table>

------

## 表达式

<table>
    <tr>
        <th>表达式</th>
        <th>Java</th>
        <th>ECMAScript</th>
        <th>Kotlin</th>
    </tr>
    <tr>
        <td>算术表达式</td>
        <td colspan="3">+、-、*、/、%</td>
    </tr>
    <tr>
        <td>赋值表达式</td>
        <td colspan="3">=、+=、-=、*=、/=、%=</td>
    </tr>
    <tr>
        <td>自增自减表达式</td>
        <td colspan="3">++、--</td>
    </tr>
    <tr>
        <td rowspan="3">关系表达式</td>
        <td colspan="3">&lt;、&gt;、&lt;=、&gt;=、==、!=</td>
    </tr>
    <tr>
        <td rowspan="2">--</td>
        <td colspan="2">
            <code>in运算符</code>
            <pre>
// JavaScript
"x" in { x:1, y:2}
// Kotlin
1 in 0..5
            </pre>
        </td>
    </tr>
    <tr>
        <td>
            <ol>
                <li><code>==</code>运算符比较两个操作数的值,<strong>可以允许操作数进行类型转换</strong></li>
                <li><code>===</code>运算符首先比较两个操作数的值,然后比较两个操作符的类型,<strong>不允许进行类型转换</strong></li>
                <li><code>!==</code>运算符是<code>===</code>运算符的取反</li>
            </ol>
        </td>
        <td></td>
    </tr>
    <tr>
        <td>逻辑表达式</td>
        <td colspan="3">&&、||、!</td>
    </tr>
    <tr>
        <td>区间表达式</td>
        <td>--</td>
        <td>--</td>
        <td>
            <strong>说明:顺序是指a&lt;b;倒序是指a&gt;b</strong>
            <ol>
                <li>闭区间表达式</li>
                <ol>
                    <li>a..b(只支持顺序[a,b])</li>
                    <li>a.rangeTo(b)(只支持顺序[a,b])</li>
                    <li>a downTo b(只支持倒序[b,a]))</li>
                </ol>
                <li>半闭区间表达式</li>
                <ol>
                    <li>a until b(只支持顺序[a,b))</li>
                </ol>
                <li>step表达式(<strong>指定区间步长</strong>)
                    <pre>
<a href="https://pl.kotl.in/GK57wuhLU">运行代码</a><br/>
for (num in 1..10 step 2) {
    print("$num ") // 输出1 3 5 7 9
}
                    </pre>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>安全表达式</td>
        <td>--</td>
        <td>--</td>
        <td>
            <ol>
                <li>判空操作符?:var s : String? = null</li>
                <li>
                    强判断操作符!!(如果希望抛出KotlinNullPointerException,则需要使用强判断操作符,而且定义的变量必须可容纳null):
                    <code>
                        var s : String? = null 
                            print(s!!)
                    </code>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>类型表达式</td>
        <td>instanceof关键字
            <pre>
Date d = new Date();
if(d instanceof Date){
    println("d是Date类")
}                
            </pre>
        </td>
        <td>instanceof运算符
            <pre>
var d = new Date();
d instanceof Date;  // true
            </pre>
        </td>
        <td>
            <ol>
                <li>
                    is表达式类似java的instanceof关键字,!is则是is表达式的否定形式
                    <code>println(2 is Int)</code>
                </li>
                <li>
                    显式类型转换表达式as和as?,as转换失败会提示异常,as?则会返回null
                    <code>println('0' as? Int)</code>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>属性名表达式</td>
        <td>--</td>
        <td>
            <table>
                <tr>
                    <th>ES5</th>
                    <th>ES6</th>
                </tr>
                <td>--</td>
                <td>用表达式作为属性名,要将表达式放在方括号之内<code>obj[attr]</code>
                    <pre>
obj['user'+'name']                        
                    </pre>
                    <blockquote>
                        <strong>注意，属性名表达式与简洁表示法，不能同时使用，会报错</strong>
                    </blockquote>
                </td>
            </table>
        </td>
        <td>--</td>
    </tr>
        <td>扩展运算符</td>
        <td>--</td>
        <td>
            <table>
                <tr>
                    <td>ES5</td>
                    <td>ES6</td>
                </tr>
                <tr>
                    <tr>
                        <td>--</td>
                        <td>扩展运算符<code>...</code>取出参数对象的所有可遍历属性，拷贝到当前对象之中
                            <pre>
let {id,...userinfo} = {id:1,username:"john",age:12,phone:"13886452132"}
toJson = () =>{
    return JSON.stringify(userinfo);
}
console.log(`id为${id},用户信息为${toJson()}`)
                            </pre>
                        </td>
                    </tr>
                </tr>
            </table>
        </td>
        <td>--</td>
    </tr>
</table>

------

## 语句

<table>
    <tr>
        <th>语句</th>
        <th>Java</th>
        <th>ECMAScript</th>
        <th>Kotlin</th>
    </tr>
    <tr>
        <td rowspan="2">if</td>
        <td colspan="3">
            作为语句
            <pre>
if(type == "1"){
    ...
}else if(type == "2"){
    ...
}else{

}
            </pre>
        </td>
    </tr>
    <tr>
        <td colspan="2">--</td>
        <td>
            作为表达式可以替代java的三元表达式:
            <pre>
<a href="https://pl.kotl.in/9MUDxrbaP">运行代码</a><br/>
val max = if(a > b) a else b
println(max)
            </pre>
        </td>
    </tr>
    <tr>
        <td>switch</td>
        <td colspan="2">
            <pre>
switch(action){
    case ACTION_DOWN:
        break;
    case ACTION_UP:
        break;
    default:
        break;    
}               
            </pre>
        </td>
        <td>
            使用when表达式替代了switch:
            <ol>
                <li>分支条件可以是任意表达式</li>
                <li>
                    分支条件的else分支相当于switch的default分支
                    <pre>
<a href="https://pl.kotl.in/4iOn-cmEY">运行代码</a><br/>
var x = Random().nextInt(1500)
when (x) {
    in 1 until 10 -> print("$x 是一位整数")
    in 10 until 100 -> print("$x 是两位整数")
    in 100 until 1000 -> print("$x 是三位整数")
    else -> print("$x 是其他整数")
}
                    </pre>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>for</td>
        <td>支持fori和foreach循环
            <ol>
                <li>fori
                    <pre>
for(int i = 0; i &lt; 10; i++ ){
    ...
}                        
                    </pre>
                </li>
                <li>foreach
                    <pre>
for(String s : StringList){
    ...
}                        
                    </pre>
                </li>
            </ol>            
        </td>
        <td>
            <table>
                <tr>
                    <th>ES5</th>
                    <th>ES6</th>
                </tr>
                <tr>
                    <td>支持fori和for...in循环
                        <ol>
                            <li>fori
                                <pre>
for(let i = 0; i &lt; 10; i++ ){
    ...
}                                    
                                </pre>
                            </li>
                            <li>for...in更方便遍历对象属性成员
                                <pre>
const arr = ['a','b','c']
arr.name = 'curry';

for(let key in arr){
  console.log(key);
}
//"0","1","2","name"         
                                </pre>
                            </li>
                        </ol>
                    </td>
                    <td>新增for...of循环
                        <ol>
                            <li>for...of遍历具有<code>iterator</code>接口的数据结构</li>
                            <li>包括数组、Set、Map、字符串、Generator 对象以及某些类似数组的对象</li>
                            <li><strong>for...in遍历获得键名,for...of遍历获得键值</strong>
                                <pre>
const arr = ['a','b','c']
arr.name = 'curry';

for(let value of arr){
  console.log(value);  
} 
//"a","b","c"                     
                                </pre>
                            </li>
                        </ol>
                    </td>
                </tr>
            </table>
        </td>
        <td>
            <ol>
                <li>只支持for...in循环</li>
                <li>for...in循环可以对提供iterator的对象进行遍历</li>
                <li>如果在数字区间上进行迭代,请使用区间表达式</li>
                <pre>
<a href="https://pl.kotl.in/DSqeDOUsb">运行代码</a><br/>                
for (i in 6 downTo 0 step 2) {
    println(i)
}
                </pre>
                <li>如果在数组或集合上进行迭代,可以使用<code>withIndex</code>函数</li>
                <pre>
<a href="https://pl.kotl.in/DSqeDOUsb">运行代码</a><br/>   
var array = arrayOf&lt;Int&gt;(1,2,3,4,5)
for ((index, value) in array.withIndex()) {
	println("the element at $index is $value")
}
                </pre>
            </ol>
        </td>
    </tr>
    <tr>
        <td>while</td>
        <td colspan="3">
            <pre>
while(count &lt; 20){
    ...
    count++;
}                
            </pre>
        </td>
    </tr>
    <tr>
        <td>break和return</td>
        <td colspan="3">break 和 continue 语句用于在循环中精确地控制代码的执行</td>
    </tr>
</table>

# 类与对象
<table>
    <tr>
        <th rowspan="2">类与对象</th>
        <th rowspan="2">Java</th>
        <th colspan="2">ECMAScript</th>
        <th rowspan="2">Kotlin</th>
    </tr>
    <tr>
        <th>ES5</th>
        <th>ES6</th>
    </tr>
    <tr>
        <td>类声明</td>
        <td></td>
        <td><pre>function Person(name) {...}</pre></td>
        <td><pre>class Person { ... }</pre></td>
        <td><pre>class Invoice { ... }</pre></td>
    </tr>
    <tr>
        <td>创建对象</td>
        <td>构造函数模式
            <pre>
Customer customer = new Customer("Joe Smith")
            </pre>
        </td>
        <td>
            <ol>
                <li>构造函数模式
                    <pre>
<a href="https://codepen.io/zero_bubble/pen/rEpabK/">运行代码</a><br/> 
function Person(name, age, job){
    
        this.name = name;
        this.age = age;
        this.job = job;
        this.sayName = function(){
            alert(this.name);
}; }

var person = new Person("Joe Smith", 29, "Software Engineer")

console.log(JSON.stringify(person))
                    </pre>
                </li>
                <li>结合原型模式,<strong>只要创建了一个新函数，就会根据一组特定的规则为该函数创建一个 prototype 属性</strong>
                    <ol>
                        <li>让所有对象实例共享它所包含的属性和方法</li>
                        <li>如果我们在实例中添加了一个属性，而该属性与实例原型中的一个属性同名，那我们就在实例中创建该属性，<strong>该属性将会屏蔽原型中的那个属性</strong>。通过<code>hasOwnProperty</code>方法区分属性存在于实例中还是存在于原型中</li>
                        <li>实例的内部将包含一个指针<code>[Prototype]</code>,指向构造函数的原型对象</li>
                    </ol>
                    <pre>
function Person(name, age, job){
&Tab;this.name = name;
&Tab;this.age = age;
&Tab;this.job = job;
}

Person.prototype = {
&Tab;constructor : Person,
&Tab;sayName : function() {
&Tab;&Tab;alert(this.name);
&Tab;}
}; 

var person = new Person("Joe Smith", 29, "Software Engineer")

console.log(JSON.stringify(person))
                    </pre>
                </li>
                <li>使用对象字面量<code>{}</code>
                    <pre>
var person = {
&Tab;firstName:"Bill",
&Tab;lastName:"Gates",
&Tab;age:62,
&Tab;eyeColor:"blue"
};                        
                    </pre>
                </li>
                <li>通过<code>Object()</code>函数
                    <pre>
var person = new Object();
person.name = "nick";
person.age = 12;
person.sayHi = function(){
    alert("Hello")
}
                    </pre>
                </li>
                <li>通过函数<code>Object.create()</code>
                    <pre>
var person1 = Object.create(person);
person1.name = "john";
                    </pre>
                </li>
            </ol>
        </td>
        <td> ES6 的class可以看作只是一个语法糖
            <pre>
class Person{
    constructor(name,age){
        this.name = name;
        this.age = age;
    }

    toString(){
        return this.name+this.age;
    }
} 

let person = new Person("john",12)
            </pre>
        </td>
        <td>构造函数模式
            <strong>注意:kotlin中没有new关键字</strong>
            <pre>
val customer = Customer("Joe Smith")
            </pre>
        </td>
    </tr>
    <tr>
        <td>构造函数</td>
        <td></td>
        <td>
            <ol>
                <li>表示如下:
                    <pre>
function Person(name) {
    this.name = name;
}
                    </pre>
                </li>
                <li>和普通函数的区别是构造函数的首个字母大写</li>
                <li>实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。
                    <pre>
this.name = name;
Person.prototype.age = 12;                        
                    </pre>
                </li>
            </ol>
        </td>
        <td>
            <ol>
                <li>表示如下:
                    <pre>
constructor(name) {
    this.name = name;
}
                    </pre>
                </li>
                <li>如果没有显示定义构造函数,会默认添加一个空构造函数</li>
                <li>实例的属性除非显式定义在其本身（即定义在this对象上），否则都是定义在原型上（即定义在class上）。
                    <pre>
this.name = name;
Person.prototype.age = 12;                        
                    </pre>
                </li>
                <li>实例的属性还可以在类的最顶层定义
                    <pre>
class Person{
    name = "";
}                        
                    </pre>
                </li>
            </ol>
        </td>
        <td>
            <ol>
                <li>主构造函数
                    <ol>
                        <li>可忽略<code>constructor</code>关键字
                            <pre>
class Person <del>constructor</del>(firstName: String) { ... }
                            </pre>
                        </li>
                        <li>不可忽略<code>constructor</code>关键字(<strong>构造函数有注解或可见性修饰符</strong>)
                            <pre>
class Customer public <strong>@Inject</strong> constructor(name: String) { …… }
                            </pre>
                        </li>
                        <li>主构造函数不能包含任何代码,初始化放在<code>init</code>代码块中
                            <pre>
<a href="https://pl.kotl.in/BCPwFm3EP">运行代码</a><br/>                                
class Person(name: String) {
    val firstProperty = "First property: $name".also(::println)
    init {
        println("First initializer block that prints ${name}")
    }
    val secondProperty = "Second property: ${name.length}".also(::println)                    
    init {
        println("Second initializer block that prints ${name.length}")
    }
}                          
                            </pre>                                  
                        </li>
                    </ol>
                </li>
                <li>
                    次构造函数</br>
                    <blockquote>委托给主构造函数会作为次构造函数的第一条语句,因此所有初始化块中的代码都会在次构造函数体之前执行。即使该类没有主构造函数，这种委托仍会隐式发生。</blockquote>
                    <pre>
class Person(val name: String) {
    constructor(name: String, parent: Person) : <strong>this(name)</strong> {
        parent.children.add(this)x
    }
}
                    </pre>
                </li>
                <li>
                    <ol>
                        <li>私有主构造函数
                            <pre>
class Customer <strong>private</strong> @Inject constructor(name: String) { …… }
                            </pre>                            
                        </li>
                        <li>私有次构造函数
                            <pre>
class Customer @Inject constructor(name: String) { 
    <strong>private</strong> constructor(name: String, age: Int) : this(name) {
        println("私有次构造函数")
    }
}                               
                            </pre>
                        </li>
                    </ol>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>继承</td>
        <td>
            <ol>
                <li>所有类的共同基类是<code>Object</code></li>
                <li>通过<code>extends</code>关键字继承
                    <pre>
public class Derived extends Base {
    ....
}
                    </pre>
                </li>
            </ol>
        </td>
        <td>通过修改原型链实现继承
            <ol>
                <li></li>
                <li><strong>继承机制实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）</strong></li>
                <li></li>
            </ol>
        </td>
        <td>通过<code>extends</code>关键字实现继承
            <ol>
                <li>表示如下:
                    <pre>
class Man extends Person{
    ....
}                        
                    </pre>
                </li>
                <li><strong>继承机制实质是先将父类实例对象的属性和方法，加到this上面（所以必须先调用super方法），然后再用子类的构造函数修改this。</strong>
                    <pre>
class Man extends Person{
    constructor(sex){
        super() // <strong>必须在this调用之前</strong>
        this.sex = sex;
    }
}                        
                    </pre>
                </li>
                <li>作为函数时，super()只能用在子类的构造函数之中，用在其他地方就会报错
                    <pre>
class Man extends Person{
    toString(){
        super(); // <strong>会报错</strong>
    }
}                             
                    </pre>
                </li>
                <li>super作为对象时，在普通方法中，指向父类的原型对象。<strong>定义在父类实例上的方法或属性，是无法通过super调用的。</strong>
                    <pre>
class Man extends Person{
    toString(){
        console.log(super.name); // undefined
        super.toString();
    }
}     
                    </pre>
                </li>
                <li>用在静态方法之中，这时super将指向父类，而不是父类的原型对象。</li>
            </ol>
        </td>
        <td>
            <ol>
                <li>所有类的共同基类是<code>Any</code></li>
                <li>通过冒号继承
                    <pre>
open class Base(p:Int)                  
class Derived(p:Int) : Base(p)  
                    </pre>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>重写</td>
        <td></td>
        <td></td>
        <td></td>
        <td>
            <ol>
                <li>重写方法
                    <blockquote>
                    <ol>
                        <li>
                            父类需要重写的方法需为 <code>open</code>
                        </li>
                        <li><strong>子类重写父类的方法必须加上 <code>override</code> 修饰符</strong></li>
                    </ol>
                    <pre>
open class Base {
    open fun v() { ... }
}
class Derived() : Base() {
    override fun v() { ... }
}
                    </pre>
                    </blockquote>
                </li>
                <li>重写属性
                    <blockquote>
                        <ol>
                            <li>前提条件和重写方法一致</li>
                            <li>可以用一个 <code>var</code> 属性覆盖一个 <code>val</code> 属性，但反之则不行。这是允许的，因为一个 <code>val</code> 属性本质上声明了一个 getter 方法，而将其覆盖为 <code>var</code> 只是在子类中额外声明一个 setter 方法。</li>
                        </ol>
                    <pre>
open class Base {
    open val x: Int get() { …… }
}
class Derived() : Base() {
    override val x: Int = ……
}                    
                    </pre>
                    </blockquote>
                </li>
            </ol>
        </td>
    </tr>
</table>
