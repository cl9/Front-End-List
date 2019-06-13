# 数据类型

| 数据类型  | Java | JS | Kotlin | Python |
| :-------------: |:-------------:| :-------------:| :-------------:|:-------------:|
| 字符串  | 1. 字符串是引用类型  | String | `String`类型:<br/>1. 可以使用`+`拼接:`val s = "abc"+1`<br/> 2. 转义字符使用传统的反斜杠方式<br/> 3. 保留原始字符串`"""`:`"""for(c in "foo") print (c)"""`<br/> 4. 字符串模版(**Kotlin推荐的字符串拼接**): `val s = "Kotlin" print("$s.length is ${s.length}")` | 
| 数字 | byte、short、int、long、float、double |`Number`类型:JS的数字类型基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(263 -1) 到 263 -1）。**它并没有为整数给出一种特定的类型** |1. 内置类型:Byte、Short、Int、Long、Float、Double<br>2. **数值常量字面值不支持八进制**<br/>3. 浮点数字面值默认double,float的表示方法和Java一样使用f或F:`123.2f`<br/> 4. 数字字面值可以使用下划线更易读:`100_000_000`<br/>5. **较小的类型不能隐式类型转换为较大的类型** |
| 布尔 | boolean | Boolean | `Boolean`类型:true或false |
| 字符 | char | -- | `Char`类型:<br/>1. 不能直接当作数字<br/>2. 可使用toInt()转换 |
| 空 | -- | Null | |
| 未定义 | -- | Undefined | | 
| 代表 | -- | `Symbol`:一种实例是唯一且不可改变的数据类型 | -- |

# 表达式

| 表达式  | Java | JS | Kotlin | Python |
| :-------------: |:------------- | :------------- | :------------- |:-------------:|
| if  | if | if | <ol><li>作为语句与java一样<br/></li><li>作为表达式可以替代java的三元运算符:`val max = if(a > b) a else b`</li></ul> | 
| switch | switch | switch | 使用when表达式替代了switch:<ol><li>分支条件可以是任意表达式</li><li>分支条件的else分支相当于switch的default分支</li></ol><strong>when (x) {<br/>&nbsp;&nbsp;in 1..10 -> print("x is in the range")<br>&nbsp;&nbsp;in validNumbers -> print("x is valid")<br>&nbsp;&nbsp;!in 10..20 -> print("x is outside the range")<br/>&nbsp;&nbsp;else -> print("none of the above")<br/>}</strong> |
| for | 支持fori和foreach循环 | for | <ol><li>只支持forin循环</li><li>forin循环可以对提供iterator的对象进行遍历</li></ol><strong>for(i in 0..9)<br/> &nbsp;&nbsp;print(i)</strong> |
| while | while | while | while循环与java一样 |


