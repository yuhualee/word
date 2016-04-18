## mac svn命令行

1. **将文件checkout到本地目录：**

	```
	svn checkout path(svn://192.168.1.1/pro/domain)    //简写svn co
	```
	
* **添加文件add**

	```
	svn add file(test.html)       
	svn add  *.html
	svn add .   
	```
	
* **提交改动**

	```
	svn commit -m "说明"  test.html    //简写svn ci 
	```
	
* **加锁/解锁**

	```
	svn lock -m "说明"  test.html    //加锁
	svn unlock test.html    //解锁
	```
	
* **更新到某个版本**

	```
	svn update -r m test.html 
	//svn update如果后面没有目录，默认将当前目录以及子目录下的所有文件都更新到最新版本。
	//svn update -r 200 test.php(将版本库中的文件test.php还原到版本200)
	//svn update test.php(更新，于版本库同步。如果在提交的时候提示过期的话，是因为冲突，需要先update，修改文件，然后清除svn resolved，最后再提交commit)
	```
	
	> 简写： `svn up`
	
* **查看状态**

	```
	svn status  test.html   //m: 修改   C: 冲突    A：预定加入到版本库   K；补锁定
	```
	> 简写：   `svn st`
	
* **删除文件：**

	```
	svn delete test.html -m "删除说明"	
	```
	
	相当于：
	
	```
	svn delete test.html
	svn commit -m "说明" test.html
	```
	
	> 简写：`svn (del,remove,rm)`
	
* **查看日志**

	```
	svn info path
	```
	
* **比较差异**

	```
	svn diff test.html
	svn diff -r m:n path(对版本m和版本n比较差异)
	```
	
* **合并**

	```
	svn merge -r m:n test.html
	```
	
* **svn帮助**

	```
	svn help
	```
	
* **恢复本地修改**

	```
	svn revert 恢复原始未改变的工作副本文件
	```