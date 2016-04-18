* 图解

	![git图解](http://image.beekka.com/blog/2014/bg2014061202.jpg)。
	
* **git clone**

	```
	git clone <版本库的网址> <本地目录名>
	```

* **git remote**

	用于管理主机名，不带选项的时候，git remote列出所有远程主机


	```
	git remote
	```
	
	查看远程主机的网址
	
	```
	git remote -v
	```
	
	查看主机的详情信息
	
	```
	git remote show <主机名>
	```
	
	用于添加远程主机
	
	```
	git remote add <主机名> <网址>
	```
	
	用于删除远程主机 
	
	```
	git removte rm <主机名>
	```
	
	用于远程主机改名
	
	```
	git remote rename <原主机名> <新主机名>
	```



* **git fetch**

	远程主机上有更新，需要将这些更新取回本地
	
	```
	git fetch <远程主机名>
	```
	
	默认取回所有分支的更新，如果想取回特定分支的更新，可以指定分支名
	
	```
	git fetch <远程主机名> <分支名>
	```
	
	查看远程分支
	
	```
	git branch -r   //查看远程分支
	git branch -a   //查看所有分支
	```


* **git pull**

	取回远程主机某个分支的更新，再与本地的指定分支合并。
	
	```
	git pull <远程主机名> <远程分支名>:<本地分支名>
	```
	
	比如，远程主机上的next分支与本地的master分支合并
	
	```
	git pull origin next:master
	```
	
	如果远程分支与当前分支合并，则冒号后面的部分可以省略。
	
	```
	git pull origin next
	```


* **git push**

	git push命令用于将本地分支的更新，推送到远程主机
	
	```
	git push <远程主机名> <本地分支名>:<远程分支名>
	```
	
	如果本地分支为空，则表示删除远程分支
	
	```
	git push origin :master
	//等同于如下
	git push origin --delete master
	```
	
	
* **gitignore**

	新建一个文件.gitignore，把不需要提交的文件写在这个文件中，就可以避免上传。

	
	
	