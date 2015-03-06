# ued文档---配置环境 #

## 首次开发环境配置


* **安装 homebrew**
	
	```
	brew -v 
	```
	查看版本，没有则安装
		
	```
	ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	```
	
	如果是 OS X 10.10 安装后可能运行不了 可参照 http://www.mseri.me/fix-hombrew-on-os-x-yosemite/
	
	```
	vim /usr/local/Library/brew.rb // 将 1.8 改为 2.0
	```
	
* **安装 nodejs**

	```
	node -v
	```
	
	查看版本，没有则安装
	
	```
	brew install node
	```
	
* **安装bower和gulp**

	```
	npm install -g bower gulp	
	```
	
	可同时安装多个，中间添加空格

* **项目构造工具**

	参考：[web app generator](https://github.com/yeoman/generator-gulp-webapp)


	```
	yo -v 
	```
	查看版本，没有则安装，如下：

	```
	npm install -g yo
	npm install -g generator-gulp-webapp
	yo gulp-webapp
	```
	
* **安装 node 插件**

	```
	node install
	```

	
* **安装用到的包**

	比如项目中用到：zepto

	```
	bower search zepto
	```
	
	选择你想用的那一个
	
	```
	bower install zeptojs --save  
	```
	
	//同上所所示
	
	```
	bower search swipe
	bower install swipejs
	```
	
	> 后面添加 “--save”,会把这些相应的配置保存在 bower.json文件里面，如下：
	
	```
	{
		 "name": "h5app",  
		 "private": true,
		 "d ependencies": {
		 	"modernizr": "~2.8.1",
		 	"pjax": "~0.1.4",
		 	"jquery": "~2.1.3",
		 	"swipejs": "~2.0.0",
		 	"zeptojs": "~1.1.6"
		 }
	}
	```
	
* **需要提交的代码**

	一般情况下我们需要提交的代码：
	
	```
	app
	dist
	bower.json
	gulpfile.js
	package.json
	```
	
	我们可以把不需要提交的东西写在文件.gitignore里面，本项目中不需要提交的文件如下：
	
	```
	.gitignore
	.DS_Store
	/node_modules/*
	/bower_components/*
	/.sass-cache/*
	/.tmp/*
	```

	
## other

* 我们只需要首次开发时，配置环境，其它时候，只需要，checkout项目，然后执行：


	```
	npm install
	bower install  
	```   
	
	> 因为在我们之前的环境中已经配置好了，只需要按配置文件里面的要求加载我们需要的内容。

	
	






