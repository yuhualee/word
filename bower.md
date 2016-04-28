
* 作用

	bower: A package manager for the web，主要作用是为模块的安装，升级和删除，提供一种统一的，可维护的管理模式。

* 安装

	```
	npm install -g bower
	```
	
* 作用及命令

	```
	bower search jquery  //搜索
	bower install  jquery   //直接按指定的用户名安装
	bower install jquery/juqery  //用户名项目名
	bower install git://github.com/user/package.git  //git 地址
	bower install http://example.com/script.js   网址
	```
	
	> 所谓安装包文件，就是将模块（以及其依赖的模块）下载到bower_components子目录中。
	
	```
	bower update jquery
	```
	> 更新jquery，如果不给出具体的模块名，则更新所有。
	
	```
	bower uninstall jquery   //卸载
	```
	
#### bower

* **创建bower.json**

	我们可以使用 bower init 创建 bower.json


	```
	bower init
	```
* **维护依赖**

	能够将包安装到你的项目中，同时将依赖关系写入到 bower.json 的 dependencies 数组。


	```
	bower install package --save
	```