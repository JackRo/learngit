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
		//回退到某个commit id号为a2e368db的版本，
		//这需要git log查看commit id号
		git reset --hard a2e368db  
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
		//如果确定删除正确则提交，如果误删，
		//则撤销删除，执行 git checkout -- [file]
		git commit -m 'delete file' 
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
16. branch命令

		git checkout -b dev // -b表示创建并切换到dev分支，相当于以下两条命令

		git branch dev //创建分支dev
		git checkout dev //切换到分支dev
		
		git branch //查看当前分支
		git merge dev //合并分支dev到当前分支
		git branch -d dev //删除分支dev
17. 查看分支合并图

		git log --graph
		git log --graph --pretty=oneline --abbrev-commit
18. 分支管理策略

		//--no-ff参数表示禁用Fast forward模式merge，使用普通模式合并，
		//合并后的历史有分支，能看出来曾经做过合并，而fast forward合并
		//就看不出来曾经做过合并。
		git merge --no-ff -m "merge with no-ff" dev
19. bug分支

		//修复bug时，我们会通过在master分支创建新的bug分支进行修复，然后合并，最后删除
		//当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，
		//再git stash pop，回到工作现场。
		git stash //保存当前工作现场
		git stash list //查看工作现场list
		git stash apply //恢复工作现场，但是恢复后，stash内容不删除
		git stash drop //删除工作现场
		git stash pop //恢复工作现场同时删除工作现场
		git stash apply stash@{0} //恢复某个工作现场
20. feature分支

		git branch -D [name] //强行删除分支
21. 多人协作

		//查看远程库信息
		git remote 
		//查看更详细的远程库信息，可以显示抓起和推送的地址，如果没有推送权限，就看不到
		//push的地址
		git remote -v
		//master分支是主分支，因此要时刻与远程同步
		//dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步
		//bug分支只用于在本地修复bug，就没必要推到远程了
		//feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发
		git push origin master //推送本地指定分支，master也可以是dev分支，bug分支等
		git checkout -b dev origin/dev //创建远程分支dev到本地
		//指定本地dev分支与远程origin/dev分支的链接
		git branch --set-upstream dev origin/dev
		git pull //拉取远程仓库最新的提交
22. 