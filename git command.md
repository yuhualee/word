 git command

* **git add**

	* git add . 将文件暂存到stage，文件创建，修改，不包含删除
	* git add -A 或者 git add -all，提交所有，包含删除
	* git add -u ，或者git add --update ,提交修改和删除，不包含新文件
	* git add -i 进入互动模式（不理解）
	* git add filename 新增一个，多个，并列往后写
	* git add -ignore-removal  忽略删除的文件
	   
	
* **git rm filename**  删除文件
	
* **git mv filename newfilename** 修改文件名
	
* **git status**  查看状态

* **git commit**

	* git commit -m "message"  提交，带说明 
	* git commit -a -m 'message' 
	* git commit -a -v 查看修改的内容
	
	
* **git branch**	

	* git branch: 查看所有分支
	* git branch new-branch: 新建分支
	* git branch new-branch master: 由master产生新的分支
	* git branch -d branch-name: 删除分支
	* git branch -D branch-name: 强制删除分支 
	* git checkout -b new-branch: 创建并切换新分支 
	* git branch -r: 列出所有 repository branch
	* git branch -a: 列出所有分支
	
* **git checkout**

	* git checkout branch-name 切换分支
	* git checkout -b new-branch: 创建并切换新分支 
	* git checkout -b new-branch branch-name: 从branch-name创建新分支并切换
	* git checkout filename: 还原文件到repository状态
	* git checkout HEAD: 将所有文件都checkout出来   
	* git checkout xxxx . #xxxx 是commit的编号的前四位，将xxxx编号的版 本checkout出来
	* git checkout – * #恢复上一次 commit的状态
	
* **git diff**

	* git diff master: 与master对比哪些文件不同
	
* **git stash**  放进暂存区

	* git stash: 放进暂存区stage
	* git stash list: 列出暂存区的文件
	* git stash pop: 取出，并移除
	* git stash apply: 取出，但不移除
	* git stash clear；清除
	
* **git reset**

	* git reset -hard HEAD^  还愿到前一版本

	
* **git revert**

	* git revert HEAD 回到前一次commit状态
	* git revert HEAD^ 回到上上一次commit状态,^可以是多个


* **git remote**

	* git remote 查看远程库的信息
	* git remote -v 查看更详细的信息
	* git remote show 列出现在有多少repository
	* git remote rm new-branch 删除远程服务器上的新分支 
	* git remote update #更新所有repository branch
	* git remote add new-branch git@github.com:yuhualee/yourRepo.git 增加远程repository的branch。
	



参考

[git 常用命令解释](http://wenku.baidu.com/link?url=TGC6XmH1wbUuNQzNnx0kqjHlQxCAeCxFWkae1VBzAmptXYHsKvb9mACtPeNvcdX57tWnRlg8kmDS5HIxNfiTpJfYSqTG-9yQcQJK95jzH87)