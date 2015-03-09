# git使用教程

## git简介

* 版本控制系统

## git 安装

* 查看git是否安装

	```
	git
	```
	
* 安装：
	
	* Linux上安装
	
		```
		sudo apt-get insall git
		```
	
	* Mac OS X上安装git
	
		* 通过homebrew
	
			```
			brew -v
			```
			```
			ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
			```
			```
			brew install git
			```
			
		* 通过Xcode，来安装：就是直接从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。
		
	* 在Windows上安装git (省略...)
	
## 使用git
	
	
* 配置git（本地mac开发环境ssh连接git）

	1. 首先在本地创建ssh key
		
		```
		ssh-keygen -t rsa -C "550807257Qqq.com"
		```

	2. 获取创建的公钥
	
		```
		cat ~/.ssh/id_rsa.pub
		```
	
	3. 进入到github个人中心，点击左侧的"SSH keys"，点击“Add SSH key”，添加进去。
	
	4. 检测，是否成功：
	
		```
		ssh -T git@github.com
		```

* 设置用户username和email：

	```
	git config --global user.name 'yuhualee'
	git config --global user.email '550807257@qq.com'
	```

* 进入要上传的仓库，添加远程地址：

	```
	git remote add origin git@github.com:yuhualee/yourRepo.git
	```
	> yourRepo.git 要替换成你自己的
	
* 初始化一个仓库

	```
	git init
	```


* 提交，上传

	```
	git status  //查看文件变化
	git add ./  //提交文件
	git commit -m "updata"   //提交
	```	
	
## git 命令

* git log 查看日志

	```
	git log
	```
	
	```
	git log --pretty=oneline
	```


* 版本回退

	```
	git reset --hard HEAD^
	```
	
	> HEAD^  几个^就代表几个版本，也可以用版本号
	
* 添加到暂存区

	```
	git add
	```
* 版本对比

	```
	git diff HEAD -- readme.txt
	```


* git status 查看文件变化
* git diff 可以查看修改的内容
		