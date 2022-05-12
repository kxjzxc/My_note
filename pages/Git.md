- # 教程
	- ## 查看信息
		- ```shell
		  
		  git commit -m "message"
		  git push
		  ```
	- ## 上传
		- ```shell
		  git add -A
		  git commit -m "message"
		  git push
		  ```
	- ## 分支
		- ```shell
		  git branch [分支名] # 新建分支
		  git checkout [分支名] # 切换分支
		  git push origin [分支名] # 远程没有remote_branch分支并且本地已经切换到local_branch
		  git push -u origin/remote_branch # 远程已有remote_branch分支但未关联本地分支local_branch且本地已经切换到local_branch
		  ```
	- ## 远程仓库操作
		- ```shell
		  git remote -v # 显示所有远程仓库
		  ```
- 参考文章
	- [git 分支管理 推送本地分支到远程分支等](https://blog.csdn.net/u013749540/article/details/78295420)