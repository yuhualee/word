

* **HTML模板**

	```
	babel src --out-dir build
	```
	> 上面命令可以将 src 子目录的 js 文件进行语法转换，转码后的文件全部放在 build 子目录。
	
	
* **reactDOM.render()**

	ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。

	例1：
	
	```
	ReactDOM.render(
		<h1>Hello,world!</h1>
		document.getElementById('example')
	);
	```
	
* **语法**

	1. HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写，**如例1**。
	
	2. 遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。
	
	例2：
	
	```
	var names = ['lyh','hxf','hmh'];
    ReactDOM.render(
      <div>
      {
        names.map(function(name){
          return <p>hello,{name}</p>
        })
      }
      </div>,
      document.getElementById('example')
    );
	```

	3. JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员（查看
	
	例3：
	
	```
	var arr = [
      <li>我是一只小小鸟</li>,
      <li>宝宝</li>,
      <li>爸爸</li>
    ];
    ReactDOM.render(
      <ul>{arr}</ul>,
      document.getElementById('example')
    );
	```
	
### 组件

* **React.createClass** - 生成组件类

	```
	var HelloMessage = React.createClass({
       render: function() {
         return <h1>Hello {this.props.name}</h1>;
       }
    });
    ReactDOM.render(
       <HelloMessage name="John" />,
       document.getElementById('example')
    );
	```
	> * 变量 HelloMessage 就是一个组件类。模板插入 <HelloMessage /> 时，会自动生成 HelloMessage 的一个实例。所有组件类都必须有自己的 render 方法，用于输出组件。
	
	> * 组件类的第一个字母必须大写，否则会报错，比如HelloMessage不能写成helloMessage。另外，组件类只能包含一个顶层标签，否则也会报错。
	
	> * 组件的用法与原生的 HTML 标签完全一致，可以任意加入属性，比如 <HelloMessage name="John"> ，就是 HelloMessage 组件加入一个 name 属性，值为 John。组件的属性可以在组件类的 this.props 对象上获取，比如 name 属性就可以通过 this.props.name 读取。
	
	> * 添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。
	
	> 		```
		var HelloMessage = React.createClass({
        	render: function() {
         		return <h1 className="h1">Hello {this.props.name}<p>可以这样吗</p></h1>;
	        }
    	  });
		```
		
### this.props.children

* **this.props.children** - 它表示组件的所有子节点

	

	
	