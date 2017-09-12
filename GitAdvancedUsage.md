#Git高级用法#

###git reset高级用法###

1. 删除工作空间改动代码，撤销commit，撤销git add . 。这个命令执行后，就恢复到了上一次的commit状态。
		
		git reset --hard [commit-id/HEAD^/HEAD^^/HEAD~100]
		
2. 不删除工作空间改动代码，撤销commit，不撤销git add . 。这个命令执行后，仅仅是撤回commit操作，您写的代码仍然保留。

		git reset --soft [commit-id/HEAD^/HEAD^^/HEAD~100]
		
3. 不删除工作空间改动代码，撤销commit，并且撤销git add . 。注意：这个--mixed是默认操作
	
		git reset --mixed [commit-id/HEAD^/HEAD^^/HEAD~100]
		
		git reset [commit-id/HEAD^/HEAD^^/HEAD~100] //与上面的一行命令效果相同
		