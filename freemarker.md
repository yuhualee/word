### 语法


参考： [FreeMarker基本语法知识](http://blog.csdn.net/wu209000/article/details/4222129)

* **基本**

	* ${...}：FreeMarker将会输出真实的值来替换大括号内的表达式，这样的表达式被称为interpolation（插值）。
	
	* 注释：注释和HTML的注释也很相似，但是它们使用<#-- and -->来标识。不像HTML注释那样，FTL注释不会出现在输出中（不出现在访问者的页面中），因为FreeMarker会跳过它们。
	
	* FTL标签（FreeMarker模板的语言标签）：FTL标签和HTML标签有一些相似之处，但是它们是FreeMarker的指令，是不会在输出中打印的。这些标签的名字以#开头。（用户自定义的FTL标签则需要使用@来代替#）


### 指令

* **if else**

	if、elseif和else指令可以用来条件判断是否越过模板的一个部分。condition必须计算成布尔值，否则错误将会中止模板处理。elseif和else必须出现在if内部（也就是在if的开始标签和结束标签之间）。if中可以包含任意数量的elseif（包括0个），而结束时else也是可选的[13]  。


	```
	<#if condition>
    	...
	<#elseif condition2>
	    ...
	<#elseif condition3>
	    ...
	<#else>
	    ...
	</#if>
	```
	
* **list**

	```
	假设 users 包含['Joe', 'Kate', 'Fred'] 序列：
	<#list users as user>
    	<p>${user}
	</#list>
	```
	
	> list指令执行在list开始标签和list结束标签（list中间的部分）之间的代码
	
* **include**

	```
	将版权信息单独存放在页面文件 copyright_footer.html 中：
	<hr>
	<i>
    	Copyright (c) 2000 <a href="http://www.baidu.com">Baidu Inc</a>,
	    <br>
    	All Rights Reserved.
	</i>
	```
	当需要用到这个文件时，可以使用 include 指令来插入：
	
	```
	<html>
    	<head>
        	<title>Test page</title>
	    </head>
    	<body>
        	<h1>Test page</h1>
	        <p>Blah blah...
    	    <#include "/copyright_footer.html">
	    </body>
	</html>
	```
	
* **assign**

	assign指令的用法有多种,包含创建或替换一个顶层变量,或者创建或替换多个变量等
	
	```
	<#assign name=value[in namespacehash]>
	```
	> 这个用法用于指定一个名为name的变量,该变量的值为value,
      此外,FreeMarker允许在使用assign指令里增加in子句,
      in子句用于将创建的name变量放入namespacehash命名空间中.
      
   还有以下用法：
   
   ```
   <#assign name1=value1 name2=value2 ... nameN=valueN [in namespacehash]>
   ```
   
   这个语法可以同时创建或替换多个顶层变量,此外,还有一种复杂的用法,       如果需要创建或替换的变量值是一个复杂的表达式,则可以使用如下语法格式
   
   ```
   <#assign name [in namespacehash]>capture this</#assign>
   ```
   
   在这个语法中,是指将assign指令的内容赋值给name变量.如下例子:
   
   ```
   <#assign x>
   	<#list ['星期一','星期二','星期三','星期四','星期五','星期六','星期日'] as n>
   		${n}
   	</#list>
   </#assign>
   ${x}
   ```
   上面的代码将输出：星期一 星期二 星期三 星期四 星期五 星期六 星期天 

	
* **内建函数：？.**

	内建函数很像子变量（也像Java中的方法），它们并不是数据模型中的东西，是FreeMarker在数值上添加的。为了清晰子变量是哪部分，使用?（问号）代替，.（点）来访问它们。常用内建函数的示例：
	
	```
	user?html给出user的HTML转义版本，比如&会由&amp;来代替
	```
	
* **空变量：！**

	当user不存在于数据模型时，模板将会将user的值表示为字符串 “visitor”。（当 user 存在时，模板就会表现出 ${user} 的值）：
	
	```
	<h1>Welcome ${user!"visitor"}!</h1>
	```
	
	也可以在变量名后面通过放置??来询问一个变量是否存在。将它和if指令合并，那么如果user变量不存在的话将会忽略整个问候的代码段：
	
	```
	<#if user??>
    	<h1>Welcome ${user}!</h1>
	</#if>
	```
	
	> 关于多级访问的变量，比如 animals.python.price，书写代码：animals.python.price!0当且仅当animals.python永远存在，而仅仅最后一个子变量price可能不存在时是正确的（这种情况下假设价格是0）。如果 animals或python不存在，那么模板处理过程将会以“未定义的变量”错误而停止。为了防止这种情况的发生， 可以如下这样来编写代码 (animals.python.price)!0。这种情况就是说animals或python不存在时，表达式的结果是 0。对于??也是同样用来的处理这种逻辑的；将animals.python.price??对比(animals.python.price)??来看
	
	
* **转义字符**

	* /";双引号(u0022)
	* /';单引号(u0027)
	* //;反斜杠(u005C)
	* /n;换行(u000A)
	* /r;回车(u000D)
	* /t;Tab(u0009)
	* /b;退格键(u0008)
	* /f;Form feed(u000C)
	* /l;<
	* /g;>
	* /a;&
	* /{;{
	* /xCode;直接通过4位的16进制数来指定Unicode码,输出该unicode码对应的字符.
	
	如果某段文本中包含大量的特殊符号,FreeMarker提供了另一种特殊格式:可以在指定字符串内容的引号前增加r标记,在r标记后的文件将会直接输出.看如下代码:
	
	```
	${r"${foo}"}
	${r"C:/foo/bar"}
	```
	> //输出结果是:  
	> ${foo}   
	> C:/foo/bar

---

### 变量

#### 数据模型的变量【root中的变量】

#### 模板中的变量使用【<#assign>定义的变量】

模板中的变量，是使用<#assign定义的变量，如果模板中定义的变量和模型中的变量名称一致，不是覆盖，而是隐藏

```
<#assign username="李四">
<#--此时模板中的变量的名称和模型中的变量名称一致，不是覆盖，而是隐藏-->
${username}
```

模型中的变量被隐藏后，可以使用.globals可以访问模型中的变量

```
<#--使用.globals可以访问模型中的变量-->
${.globals.username}
```

#### 局部变量【在指令中的变量】

使用local可以声明局部变量

```
<#macro test>
   <#--
   此时当调用该指令之后，会将模板中的变量username覆盖为王五
   所以这种方式存在风险，所以一般不使用这种方式在指令中定义变量
   -->
   <#--<#assign  username="王五"/>-->
   <#--使用local可以声明局部变量，所以在marco中非特殊使用局部变量-->
   <#local  username="王五"/>
   ${username}
</#macro>
<@test/>
${username}
```

#### 循环变量【在循环中的变量】

在list循环中定义的变量，循环中的变量只在循环中有效，也是一种临时的变量定义方式

```
<#list 1..3 as username>
   <#--循环中的变量出了循环就消失-->
   ${username}
</#list>
${username}
```

---

### 表达式

* **字符串**

	直接指定字符串值使用单引号或双引号限定,如果字符串值中包含特殊字符需要转义。


* **数值**

	表达式中的数值直接输出,不需要引号.小数点使用"."分隔,不能使用分组","符号.FreeMarker目前还不支持科学计数法,所以"1E3"是错误的.在FreeMarker表达式中使用数值需要注意以下几点:
	
	1. 数值不能省略小数点前面的0,所以".5"是错误的写法
	2. 数值8 , +8 , 8.00都是相同的


* **布尔值**

	直接使用true和false,不使用引号.

* **集合**

	集合以方括号包括,各集合元素之间以英文逗号","分隔,看如下的例子:
	
	```
  	<#list ['星期一','星期二','星期三','星期四','星期五','星期六','星期日'] as n>
  		${n}
 	</#list>
	```
	
	除此之外,集合元素也可以是表达式,例子如下:
	
	```
	[2 + 2, [1, 2, 3, 4], "whatnot"]
	```
	还可以使用数字范围定义数字集合,如2..5等同于[2, 3, 4, 5],但是更有效率.注意,使用数字范围来定义集合时无需使用方括号,数字范围也支持反递增的数字范围,如5..2

* **Map对象**

	Map对象使用花括号包括,Map中的key-value对之间以英文冒号":"分隔,多组key-value对之间以英文逗号","分隔.下面是一个例子:
	
	```
	{"语文":78, "数学":80}
	```
	> Map对象的key和value都是表达式,但是key必须是字符串





---
	
### 内置函数

* **Sequence**

	1. **sequence?first** - 返回sequence的第一个值。
	2. **sequence?last** - 返回sequence的最后一个值。
	3. **sequence?reverse** - 将sequence的现有顺序反转，即倒序排序
	4. **sequence?size** - 返回sequence的大小
	5. **sequence?sort** - 将sequence中的对象转化为字符串后顺序排序
	6. **sequence?sort_by(value)** - 按sequence中对象的属性value进行排序
	
	> Sequence不能为null。
	
* **Hash**

	1.  **hash?keys** - 返回hash里的所有key,返回结果为sequence
	2. **hash?values** - 返回hash里的所有value,返回结果为sequence
	
	```
	<#assign user={'name':'lyh','sex':'woman'}>
	<#assign keys=user?keys>
		${keys?last}
	<#list keys as key>
		${key}=${user[key]}
	</#list>
	```
	
* **操作字符串**

	1. substring(start,end) - 从一个字符串中截取子串
	
		> start:截取子串开始的索引，start必须大于等于0，小于等于end。end: 截取子串的长度，end必须大于等于0，小于等于字符串长度，如果省略该参数，默认为字符串长度。
		
		```
  		${'iLoveYou'?substring(4,6)}   //eY
		```
		
	2. cap_first - 将字符串的首字母变为大写
	
		```
		${'iLoveYou'?cap_first}   //ILoveYou
		```
		
	3. uncap_first - 将字符串首字母变为小写
	
		```
		${'ILoveYou'?uncap_first}  //iLoveYou
		```
		
	4. capitalize - 将字符串中的所有单词首字母变为大写
		
		```
		${'i love you'?capitalize}   //I Love You
		```
		
	5. date,time - datetime将字符串转换为日期
	
		```
		<#assign date1='2009-10-12'?date('yyyy-MM-dd')>
	    ${date1}
		<#assign date2='9:28:20'?time('HH:mm:ss')>
		${date2}
		<#assign date3='2009-10-12 9:28:20'?time('HH:mm:ss')>
		${date3}
		```
		
	* ends_with - 判断某个字符串是否由某个子串结尾，返回布尔值
	
		```
		${'string'?ends_with('ing')?string}   //true
		```
		> 布尔值必须转换为字符串才能输出，否则会报错，比如：
		
		> ```
		${'string'?ends_with('ing')}
		```
		
	* html - 将字符串中的<、>、&和"替换为对应的`&lt; &gt; &quote; &amp`
	
		```
		${'<string>'?html}   //<string>
		```
		
	* index_of（substring,start）- 在字符串中查找某个子串，返回找到子串的第一个字符的索引，如果没有找到子串，则返回-1。
	
		> Start参数用于指定从字符串的那个索引处开始搜索，start为数字值。 如果start大于字符串长度，则start取值等于字符串长度，如果start小于0， 则start取值为0。
		
		```
		${'string'?index_of('in')   //3
		${'string'?index_of('ab')    //-1
		```
		
	* length - 返回字符串的长度 `${'string'?length}`à结果为6
	
	* lower_case - 将字符串转为小写
	
		```
		${'I LOVE YOU'?lower_case}   //i love you
		```
		
	* upper_case - 转大写
	
	* contains - 判断字符串中是否包含某个子串，返回布尔值
	
		```
		${'I love you'?contains('love')?string}   //true
		```
		
		> 布尔值必须转换为字符串才能输出
		
	* number - 将字符串转为数字
	
		```
		${'11.11'?number}
		```
	* replace - 用于将字符串中的一部分从左到右替换为另外的字符串。
	
		```
		${'stabng'?replace('ab','in')}    //string
		```
		
	* split使用指定的分隔符将一个字符串拆分为一组字符串
	
		```
		<#list 'This|is|split'?split('|') as s>
			${s}
		</#list>
		//This is split
		```
		
	* trim - 删除字符串首尾空格 ${“ String ”?trim} à结果为String
	
* **操作数字**

	1. c - 用于将数字转成字符串
	
		```
		${123?c}  //123
		```
		
	* string - 用于将数字转换为字符串
	
		Freemarker中预订义了三种数字格式：number,currency（货币）和percent(百分比)其中number为默认的数字格式转换
		
		```
		<#assign tempNum=20>
			${tempNum?string.number}   //20 
			${tempNum?string('number')}   //20 
			${tempNum?string.currency}    //￥20.00 
			${tempNum?string('currency')}   //￥20.00 
			${tempNum?string.percent}    //2,000% 
			${tempNum?string('percent')}   //2,000%
		```
		
	* 数字格式化插值
	
		数字格式化插值可采用#{expr;format}形式来格式化数字,其中format可以是:
		
		* mX:小数部分最小X位
		* MX:小数部分最大X位
		
		```
		<#assign x=2.586>
		<#assign y=4>
		#{x;M2}   //2.59
		#{x;m2}   //2.59
		#{y;M2}   //4
		#{y;m2}   //4.00
		#{x;m1M2}  //2.59
		#{y;m1M2}   //4.0
		```
	

* **操作布尔值**

	* string - 用于将布尔值转换为字符串输出
	
		```
		<#assign foo=true/>
		${foo?string("yes", "no")}
		```
	
	










	
	
	
	
	
	