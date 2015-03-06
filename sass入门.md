Date: 2015-01-30  
Title: sass  
Published: true  
Type: post  
Excerpt:   



以下为工作习惯总结而出，依据个人风格不同，来写：

* **文件后缀名**

	* .sass: 不使用大括号和分号
	
		```
		body
			background:#fff
			color:#333
		p
			line-height:20px
		```
	
	* .scss: 使用括号和分号，和css差不多
	
		```
		body{
			background:#fff;
			color:#333;
		}
		p{
			line-height:20px
		}
		```

* **导入**

	```
	@import "reset"
	```
	
* **注释**

	* 标准的css注释：
	
		```
		/*标准注释*/
		```
		
	* 双斜杠单行注释：不会被翻译出来
	
		```
		//单行注释
		```


* **变量**

	* 以$开头，如果变量需要镶嵌在字符串中，需要写在#{}之中。
	
		```
		//color
		$font-color:#f90;
		$bg-color:#ccc;
		$border-color:#aaa;
		//size
		$smaller:20px;
		$normal:30px;
		$bigger:40px;
		...
		```
		
	* 多值变量：
	
		```
		$link-color: #333 #f90 #666 !default;
		a{
			color:nth($link-color,1);
			&:hover{
				color:nth($link-color,2);
			}
		}
		//编译后的css
		a{color:#333;}
		a:hover{color:#f90;}
		```
* **嵌套**

	* 选择器嵌套
	
		```
		ul{
			li{
				a{
					&:hover{
					}
				}
			}
		}
		```
	
	* 属性嵌套
	
		```
		div{
			border:{
				style: solid;
				left:{
					width:1px;
					color:#f0f0f0;
				}
				right:{
					width:2px;
					color:#f09;
				}
			}
		}
		```
		
	* @at-root
	
		```
		.parent{
			@at-root{
				.child1{
				}
				.child2{
				}
			}
		}
		//css编译结果
		parent{}
		.child1{}
		.child2{}
		```
		
		* @at-root(without:....)
		
			@at-root   |   效果
			-----------|---------------------
			all        | 所有
			rule       | 常规
			mdeia      | media
			support    | suppoert
		
			```
			//跳出父级
			@media print{
				.parent{
					@at-root .child{
					}
				}
			}
			//跳出media ,父级有效
			@media print{
				.parent{
					@at-root(without:media) .child{
					}
				}
			}
			```
		
		* @at-root与&配合使用
		
			```
			.child{
				@at-root .parent &{
				}
			}
			//css编译后
			.parent .child{}
			```

* **混合mixin**

