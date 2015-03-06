# ued--文档结构

* **css文档目录结构**

	* **目录** 
	
		```
		base/
			|-- variables.scss
			|-- mixins.scss
			|-- 
		framework/
			|-- grid.scss
			|-- layout.scss
		modules/
			|-- buttons.scss
			|-- tabs.scss
			|-- lists.scss
			|-- forms.scss
		global.scss
		```
		
		在global.scss里引入相应的文件：
		
		```
		@import "reset";
		
		@import "base/variables";
		@import "base/mixins";
		
		@import "framework/grid";
		@import "framework/layout"
		
		@import "modules/buttons"
		@import "modules/tabs"
		@import "modules/lists"
		@import "modules/forms"
		```


* **scss样式文件**


	* **variables.scss**  定义变量
	
		```
		//font
		$font-family-default: "Helvetica Neue", Helvetica, STHeiTi,Arial, sans-serif; 
		...
		
		//-----------
		//Colors: 
		
		//Main font colors
		$default-color:#333;
		$primary-color:#f60;
		$negative-color:#999;
		
		//Background colors
		bg-color:#aaa;
		border-color:#ccc;
		
		//-----------
		//Bars
		$bar-smaller-height: 20px;
		$bar-normal-height: 30px;
		$bar-biger-height:40px;
		
		//-----------
		//Borders
		$border-default: 1px solid $border-color;
		$border-radius:5px;
		```
		
	* **mixins.scss** 
	
	* **reset.scss** 样式重置
	
	* **layout.scss** 布局
	
	* **buttons.scss**  按钮
	
		```
		.btn{
			//normal style
			&:active,
			&.active{
				//stress style
			}
			&:disabled,
			&.disable{
				//disabled style
			}
			//size
			&.btn-block{
			}
			&.btn-smaller{
			}
			&.btn-bigger{
			}
			//color
			&.btn-normal{
			}
			&.btn-primary{
			}
		}
		```
		
	* **form.scss**	 表单
	