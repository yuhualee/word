# artTemplate

 javascript 模板引擎
 
* **安装** 

	```
	npm install art-template
	```

 
###  原理

* **原理**

	```
	<h3>
		<% if(typeof content === 'string'){ %>
			<%= content %>
		<% } %>
	</h3>
	```
	HTML语句与变量输出语句被直接输出，解析后的字符串类似：
	
	```
	$out.push('<h3>');
	if(typeof content === 'string'){
		$out.push(content);
	}
	$out.push('</h3>');
	```


* **编写模板**

	使用一个`type='text/html'`的script标签存放模板
	
	```
	<script src="http://aui.github.io/artTemplate/dist/template.js"></script>
	<script type="text/html">
		//code...
	</script>
	```
	
### 方法

* **template(id,data)**

	根据 id 渲染模板。内部会根据document.getElementById(id)查找模板。
	
* **template.compile**


### 语法

* **语法**

	
* **循环**

	javascript:

	```
	var data = {
		title: '标签',
		list: ['艺术','文艺','博客','摄影','电影','民谣','旅行','音乐']
	};
	$('.box').html(template('test',data));
	```
	
	html模板:
	
	```
	<script type="text/html" id="test">
		<h1><%=title%></h1>
		<ul>
			<% for(var i=0; i<list.length; i++){ %>
				<li><%=list[i]%>
			<% } %>
		</ul>
	</script>
	```