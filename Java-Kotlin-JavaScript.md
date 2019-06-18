## 在线编译网站

+ [Kotlin在线编译](https://play.kotlinlang.org/)

------

## 数据类型

<table>
    <tr>
        <th>数据类型</th>
        <th>Java</th>
        <th>JS</th>
        <th>Kotlin</th>
    </tr>
    <tr>
        <td>字符串</td>
        <td>1. 字符串是引用类型</td>
        <td>String</td>
        <td>
            <ol>
                <li>
                    可以使用<code>+</code>拼接:
                    <code>val s = "abc"+1</code>
                </li>
                <li>转义字符使用传统的反斜杠方式</li>
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
        <td>`Number`类型:JS的数字类型基于 IEEE 754 标准的双精度 64 位二进制格式的值（-(263 -1) 到 263 -1）。**它并没有为整数给出一种特定的类型** </td>
        <td>
            <ol>
                <li>内置类型:Byte、Short、Int、Long、Float、Double</li>
                <li><strong>数值常量字面值不支持八进制</strong></li>
                <li>浮点数字面值默认double,float的表示方法和Java一致使用f或F:<code>123.2f</code></li>
                <li>数字字面值可以使用下划线更易读:<code>100_000_000</code></li>
                <li><strong>较小的类型不能隐式类型转换为较大的类型</strong></li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>布尔</td>
        <td>boolean</td>
        <td>Boolean</td>
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
        <td>Null</td>
        <td>--</td>
    </tr>
    <tr>
        <td>未定义</td>
        <td>--</td>
        <td>Undefined</td>
        <td>--</td>
    </tr>
    <tr>
        <td>代表</td>
        <td>--</td>
        <td><code>Symbol</code>:一种实例是唯一且不可改变的数据类型</td>
        <td>--</td>
    </tr>
</table>

------

## 运算符

<table>
    <tr>
        <th>运算符</th>
        <th>Java</th>
        <th>JS</th>
        <th>Kotlin</th>
    </tr>
    <tr>
        <td>算术运算符</td>
        <td>+、-、*、/、%</td>
        <td>一致</td>
        <td>一致</td>
    </tr>
    <tr>
        <td>赋值运算符</td>
        <td>=、+=、-=、*=、/=、%=</td>
        <td>一致</td>
        <td>一致</td>
    </tr>
    <tr>
        <td>自增自减运算符</td>
        <td>++、--</td>
        <td>一致</td>
        <td>一致</td>
    </tr>
    <tr>
        <td>关系运算符</td>
        <td>&lt;、&gt;、&lt;=、&gt;=、==、!=</td>
        <td>一致</td>
        <td>一致</td>
    </tr>
    <tr>
        <td>逻辑运算符</td>
        <td>&&、||、!</td>
        <td>一致</td>
        <td>一致</td>
    </tr>
    <tr>
        <td>区间运算符</td>
        <td>--</td>
        <td>--</td>
        <td>
            <strong>说明:顺序是指a&lt;b;倒序是指a&gt;b</strong>
            <ol>
                <li>闭区间运算符</li>
                <ol>
                    <li>a..b(只支持顺序[a,b])</li>
                    <li>a.rangeTo(b)(只支持顺序[a,b])</li>
                    <li>a downTo b(只支持倒序[b,a]))</li>
                </ol>
                <li>半闭区间运算符</li>
                <ol>
                    <li>a until b(只支持顺序[a,b))</li>
                </ol>
                <li>step运算符(<strong>指定区间步长</strong>)
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
        <td>安全运算符</td>
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
        <td>类型运算符</td>
        <td>instanceof关键字</td>
        <td>--</td>
        <td>
            <ol>
                <li>
                    is运算符类似java的instanceof关键字,!is则是is运算符的否定形式
                    <code>println(2 is Int)</code>
                </li>
                <li>
                    显式类型转换运算符as和as?,as转换失败会提示异常,as?则会返回null
                    <code>println('0' as? Int)</code>
                </li>
            </ol>
        </td>
    </tr>
</table>

------

## 表达式

<table>
    <tr>
        <th>表达式</th>
        <th>Java</th>
        <th>JS</th>
        <th>Kotlin</th>
    </tr>
    <tr>
        <td>if</td>
        <td>if</td>
        <td>if</td>
        <td>
            <ol>
                <li>作为语句与java一致</li>
                <li>
                    作为表达式可以替代java的三元运算符:
                    <pre>
<a href="https://pl.kotl.in/9MUDxrbaP">运行代码</a><br/>
val max = if(a > b) a else b
println(max)
                    </pre>
                </li>
            </ol>
        </td>
    </tr>
    <tr>
        <td>switch</td>
        <td>switch</td>
        <td>
            switch
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
        <td>支持fori和foreach循环</td>
        <td>for</td>
        <td>
            <ol>
                <li>只支持forin循环</li>
                <li>forin循环可以对提供iterator的对象进行遍历</li>
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
        <td>while</td>
        <td>while</td>
        <td>while循环与java一致</td>
    </tr>
</table>