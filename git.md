# git使用教程

## git简介

* 版本控制系统

---


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
	
---
	
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

### 

* 在本地工作目录中初始化一个新仓库

	```
	git init
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
	

* 提交，上传

	```
	git status  //查看文件变化
	git add ./  //提交文件
	git commit -m "updata"   //提交
	```	
	
---

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


* **git status** 查看文件变化

* **git checkout -- file** ：在git add之前，撤消本次的修改
		
	这个命令里面的“--”很重要，没有这个“--”，就变成一个创建新分支的命令。
	
* **git reset HEAD file :**

	可以把暂存区的修改撤消掉，比如一个文件修改后已经运行了git add命令，添加到了暂存区。它回到了工作区，但修改并没有撤消，也就是回到了git add 之前的状态，通过git status可以查看到。
	
* **git rm file**

	删除一个文件
	
---
	
## 远程仓库

### SSH Key
	
* 第一步：创建SSH key

	```
	ssh-keygen -t rsa -C "youremail@example.com"
	```
	> 换成你的自己的邮箱，一路回车。
	
* 第二步：获取你的公钥

	```
	cat ~/.ssh/id_rsa.pub
	```
	
	> 注意，在主目录下.ssh里面有两个文件：id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心的告诉任何人。
	
* 第三步：登录gitHub，打开“Account settings”，找到“SSH Keys”，粘贴公钥。

### 添加远程库

* 在github上新建仓库 repository。

* 关联远程库：

	```
	git remote add origin git@github.com:用户名/仓库名
	```
	
* 第一次把本地库的内容推送到远程库上：

	```
	git puhs -u origin master
	```
	
	> 由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
	
### 从远程库克隆

* 创建仓库

* 克隆一个本地库

	```
	git clone git@github.com:yuhualee/css.git
	```
	
---

## 分支管理

### 创建与合并分支

* 创建分支

	```
	git checkout -b dev  //创建+切换
	```
	
	相当于以下两命令
	
	```
	git branch dev   //创建分支dev
	git checkout dev  //切换到分支dev上
	```

* 合并分支

	```
	git merge dev   //用于合并指定分支到当前分支
	```
	> git使用的是fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。
	
	```
	git merge --no-ff -m "info" dev
	```
	
	> --no-ff模式下，会生成一个新的commit，这样，从分支历史上可以查看出分支信息，因为要生成一个commit，所以加上“-m” 插入描述信息。
	
* 删除分支

	```
	git branch -d dev
	```
	
* 查看分支

	```
	git branch
	```
	
* 查看分支合并图

	```
	git log --graph
	```

### bug分支

*  比如你正在dev下开始，有修改，但不想提交，可以先存储起来:

	```
	git stash
	```
	
* 临时修改master分支上一个小bug，可以切换到该分支下：

	```
	git checkout master   //切换
	git checkout -b issue  //创建分支issue，并切换到该分支下
	```
	
* 修复后，提交 

	```
	git add .
	git commit -m "info"
	```
	
* 回到master分支，合并删除

	```
	git checkout master   //切换
	git merge --no-ff -m "info"
	git branch -d issue  //删除分支 
	```
	
* 切换到dev，找回存储的

	```
	git stash list  //查看存储列表
	git stash apply   //恢复
	git stash drop  //删除
	```
	
	```
	git stash pop   //恢复的同时删除
	```
	
	也可以恢复指定的
	
	```
	git stash apply stash@{0}
	```
> 当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。

### feature 分支

* 和bug分支类似，也可以删除

	```
	git branch -d feature
	```
	
* 也可以强行删除

	```
	git branch -D <name>
	```
	
### 多人协作

* 查看远程库的信息

	```
	git remote
	git remote -v //查看更详细的信息
	```
	
* 推送分支 

	```
	git push origin master  //后面的分支可以省略，默认是当前分支
	```
	
	> 不必要的分支不必推送，比如bug分支，feature分支
	
* 抓取分支

	```
	git clone git@github.com:yuhualee/css.git
	```
	> 从远程库上克隆分支，默认的是只能看到master分支，想要看到dev分支，需要创建
	
	```
	git checkout -b dev origin/dev
	```
	
	为避免冲突，在推送之前，先获取最新分支
	
	```
	git pull
	```
	
* 如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令

	```
	git branch --set-upstream dev origin/dev
	```
	再pull

===

## 标签管理

* 创建标签

	```
	git branch //查看分支
	git checkout master   //切换要打标签的分支
	git tag <name>   //打一个新标签
	git tag   //查看所有标签
	```
	
	有时候忘记打标签了，可以找到历史提交的commit id，被打上就可以了
	
	```
	git log --pretty=oneline --abbrev-commit    //查看log
	git tag v0.9 <commit id>	  //添加标签，指定commit id
	git show <tagname>    //查看标签信息
	```
	
	还可以创建有说明的标签
	
	```
	git tag -a <tagname> -m "version info" <commit id>   //-a指定标签名，-m指定说明文字
	```
	

* 操作标签

	```
	git tag -d v1.0   //删除本地标签
	git push origin <tagname>  //推送指定的标签到服务器
	git push origin --tags  //推送全部标签
	```
	
	如果标签已提交，要删除远程标签就麻烦一点，先从本地删除
	
	```
	git tag -d <tagname>   //本地删除
	git push origin :refs/tags/<tagname>    //远程删除
	```


## 使用github

* git全局设置

	```
	git config --global user.name "your name"
	git config --global user.email youremail@email.com
	```
	
* 将git项目与github建立联系

	```
	mkdir yourgithubproject  //创建文件夹
	cd yourgithubproject   //进入文件夹
	git init   //在本地工作目录中初始化一个新仓库
	touch README  //
	git add README  //添加
	git commit -m "注释"   //提交
	git remote add origin  git@github.com:yourgithubname/yourgithubproject.git   //首次关联的时候用，以后就不用了	git push origin master
	```

* 导入现有的git仓库

	```
	cd existing_git_project
	git remote add origin git@github.com:yourgithubname/yourgithubproject.git
	git push -u origin master
	```
	
* 克隆一个仓库

	```
	git clone git@github.com:yuhualee/css.git
	```

	
* 第一次提交

 ```
 git push yourgitproject master
 ```
 
* 日常提交

	```
	git add .
	git commit -a -m "info"
	git push
	```
      


## 命令参数

* -a 指定标签名
* -m 指定说明文字
* -s 用私钥签名一个标签









