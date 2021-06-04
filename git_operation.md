1. new a test
2. git add test
3. git commit -m "description"   ----- you can add several tests and one commit description

4. git status
5. git diff

6. git log
   git log --pretty=online

7. git reset --hard HEAD^
   git reset --hard HEAD~100

8. git reflog   //查找git的历史，找到错删的版本号
9. git reset --hard 版本号   //恢复新的版本号对应的文件
	//版本回退条件：没有推送到远程
10. 工作区working directory
    版本库 repository  //工作区隐藏目录.git，不算工作区，而是git的版本库
	//暂存区stage(index): git add 把文件修改添加到暂存区    git commit 把暂存区所有内容提交到当前分支

11. git checkout --text   //回到最近一次git add 或 git commit时的状态
12. git reset HEAD test   //撤销缓存区的修改，重新放回工作区

13. git rm test  //删除版本库中文件，git rm，然后git commit
14. git checkout -- test //一键还原误删文件

15. 远程仓库
