

### 指令

* 指令的书写方式
	
	```
	<div ng-bind="name"></div>
	<div ng:bind="name"></div>
	<div ng_bind="name"></div>
	<div data-ng-bind="name"></div>
	<div x-ng-bind="name"></div>	
	```


* **`ng-app`** angularJs的启动器

	标记了angularJs脚本的作用域，在html添加，说明整个html都是AngularJs脚本作用域，也可以局部使用，如`<div ng-app>`，则表示在div内部运行。

* **`ng-model`**

	`ng-model = 'varname'`绑定到一个叫`varname`的模型变量

* **ng-repeat**

* **`ng-bind`和`ng-bind-template`**

* **`ng-view`**

* **`{{}}`绑定表达式:** 

	绑定表达式，可以是一个字符串，也可以一个变量，还可以是一个表达式`{{varname || 'world'}}`，将结果插入到DOM中，可以随着表达式运算结果的改变而实时更新。



## 控制器 ng-controller

### 作用域(Scope): 

## 迭代器过滤 `filter`

* **orderBy:** 排序



## 进阶

路由，模块，依赖，注入

**angular.module is a global place for creating, registering and retrieving Angular modules. ngAppName is the name of this angular module example (also set in a <body> attribute in index.html)**

* html

	```
	<!doctype html>
	<body ng-app="ngAppName">
	...
	```
* app.js
	
	```
	angular.module('ngAppName',[]).
	```
* controllers.js

	```
	function nameCtrl($scope){
		$scope.nameId = {
		};
	}
	```
	
* 模板

	```
	<html lang="en" ng-app="phonecat">
	<head>
	...
  		<script src="lib/angular/angular.js"></script>
  		<script src="js/app.js"></script>
		<script src="js/controllers.js"></script>
	</head>
	<body>
  		<div ng-view></div>
	</body>
	</html>
	```



## 项目

一个完整的项目结构

```
app
|---css
|---framework
|---images
|---js
		app.js                    //作为启动点的js
		controllers.js			   //控制器  
		directives.js             //指令
		filters.js                //过滤
		services.js               //
	templates                    //片断文件
		detail.html
		list.html
	index.html                   //index.html文件
node_modules
...

```