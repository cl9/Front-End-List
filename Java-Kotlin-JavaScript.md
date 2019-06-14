
## 在线编译网站

+ [Kotlin在线编译](https://play.kotlinlang.org/)

------

## 数据类型

| 数据类型  | Java | JS | Kotlin | Python |
| :-------------: |:-------------:| :-------------:| :-------------:|:-------------:|
| 字符串  | 1. 字符串是引用类型  | String | `String`类型:<br/>1. 可以使用`+`拼接:`val s = "abc"+1`<br/> 2. 转义字符使用传统的反斜杠方式<br/> 3. 保留原始字符串`"""`:`"""for(c in "foo") print (c)"""`<br/> 4. 字符串模版(**Kotlin推荐的字符串拼接**): `val s = "Kotlin" print("$s.length is ${s.length}")` | 
| 数字 | byte、short、int、long、float、double |`Number`类型:JS的数字类型基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(263 -1) 到 263 -1）。**它并没有为整数给出一种特定的类型** |1. 内置类型:Byte、Short、Int、Long、Float、Double<br>2. **数值常量字面值不支持八进制**<br/>3. 浮点数字面值默认double,float的表示方法和Java一样使用f或F:`123.2f`<br/> 4. 数字字面值可以使用下划线更易读:`100_000_000`<br/>5. **较小的类型不能隐式类型转换为较大的类型** |
| 布尔 | boolean | Boolean | `Boolean`类型:true或false |
| 字符 | char | -- | `Char`类型:<br/>1. 不能直接当作数字<br/>2. 可使用toInt()转换 |
| 空 | -- | Null | |
| 未定义 | -- | Undefined | | 
| 代表 | -- | `Symbol`:一种实例是唯一且不可改变的数据类型 | -- |

------

## 运算符

| 运算符  | Java | JS | Kotlin | Python |
| :-------------: |:------------- | :------------- | :------------- |:-------------:|
| 算术运算符  | +、-、*、/、% | 一致 | 一致 | 
| 赋值运算符 | =、+=、-=、*=、/=、%= | 一致 | 一致 | 
| 自增自减运算符 | ++、-- | 一致 | 一致 |
| 关系运算符 | <、>、<=、>=、==、!= | 一致 | 一致 |
| 逻辑运算符 | &&、\|\|、! | 一致 | 一致 |
| 区间运算符 | -- | -- | **说明:顺序是指a<b;倒序是指a>b**<ol><li>闭区间运算符:<ul><li>a..b(只支持顺序[a,b])</li><li>a.rangeTo(b)(只支持顺序[a,b])</li><li>a downTo b(只支持倒序[b,a]))</li></ul></li><li>半闭区间运算符:a until b(只支持顺序[a,b))</li></ol> |
| 安全运算符 | -- | -- | <ol><li>判空操作符?:`var s : String? = null`</li><li>强判断操作符!!(如果希望抛出KotlinNullPointerException,则需要使用强判断操作符,而且定义的变量必须可容纳null):<strong><br/>var s : String? = null <br/>print(s!!)</strong></li></ol> | 
| 类型运算符 | instanceof关键字 | -- | <ol><li>is运算符类似java的instanceof关键字,!is则是is运算符的否定形式`println(2 is Int)`</li><li>显式类型转换运算符as和as?,as转换失败会提示异常,as?则会返回null`println('0' as? Int)`</li></ol> |

------

## 表达式

| 表达式  | Java | JS | Kotlin | Python |
| :-------------: |:------------- | :------------- | :------------- |:-------------:|
| if  | if | if | <ol><li>作为语句与java一样<br/></li><li>作为表达式可以替代java的三元运算符:`val max = if(a > b) a else b`</li></ul> | 
| switch | switch | switch | 使用when表达式替代了switch:<ol><li>分支条件可以是任意表达式</li><li>分支条件的else分支相当于switch的default分支</li></ol><strong>when (x) {<br/>&nbsp;&nbsp;in 1..10 -> print("x is in the range")<br>&nbsp;&nbsp;in validNumbers -> print("x is valid")<br>&nbsp;&nbsp;!in 10..20 -> print("x is outside the range")<br/>&nbsp;&nbsp;else -> print("none of the above")<br/>}</strong> |
| for | 支持fori和foreach循环 | for | <ol><li>只支持forin循环</li><li>forin循环可以对提供iterator的对象进行遍历</li></ol><strong>for(i in 0..9)<br/> &nbsp;&nbsp;print(i)</strong> |
| while | while | while | while循环与java一样 |


