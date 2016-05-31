# Git常用命令 #

1. 初始化本地仓库

		git init
2. 将文件file添加到git的暂存区

		git add [file] 
3. 将改变提交到本地git仓库，提交信息为message

		git commit -m 'message' 
4. 查看提交日志

		git log 
5. 简洁的查看提交日志，单行模式显示日志

		git log --pretty=oneline 
6. 回退版本，HEAD是一个指针，指向版本号，

		git reset --hard HEAD^  //回退到上一版本
		git reset --hard HEAD^^  //回退到上上一个版本
		git reset --hard HEAD~100  //回退到上100个版本
		git reset --hard a2e368db  //回退到某个commit id号为a2e368db的版本，这需要git log查看commit id号
7. 查看对git本地仓库的历史执行过的命令

		git reflog
8. 查看本地仓库当前版本的状态

		git status
9. 查看某个文件的内容

		cat [file]
10. 查看工作区和版本库里最新版本某文件的区别

		git diff HEAD -- README.md
11. 未添加到暂存区时，丢弃工作区里某文件file的修改

		git checkout -- [file]
12. 添加到暂存区后，想要丢弃工作区里某文件file的修改

		git reset HEAD [file] //第一步
		git checkout -- [file] //第二步
13. 删除文件

		rm [file] //删除文件第一种方法，或者直接在文件夹中删除
		git checkout -- [file] //如果这样删错了，要撤销删除，则执行此命令
		git rm [file] //删除文件第二种方法
		git commit -m 'delete file' //如果确定删除正确则提交，如果误删，则撤销删除，执行 git checkout -- [file]
14. 添加远程仓库，在本地仓库目录下执行

		//这里远程仓库名是origin，这是git的默认叫法，也可以改成别的
		git remote add origin git@github.com:JackRo/learngit.git 
		//这里加-u参数是为了把本地仓库的master分支推送到远程仓库的
		//master分支，并把本地仓库的master分支和远程仓库的master分支关联起来，
		//在以后的推送或者拉取时就可以简化命令
		git push -u origin master 
15. clone远程仓库到本地

		git clone git@github.com:JackRo/learngit.git
		git clone https://github.com/JackRo/learngit.git
16. 