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

15. 远程仓库	https://www.liaoxuefeng.com/wiki/896043488029600/896954117292416
	创建SSH Key	ssh-keygen -t rsa -C "youremail@example.com"
	主目录 -> .ssh目录 -> id_rsa（私钥) -> id_rsa.pub(公钥)
	登陆GitHub -> 打开settings -> Add SSH Key:填上title,粘贴id_rsa.pub文件
16. 添加远程库
	git remote add origin git@github.com:tianxin5750/learngit.git
	git push -u origin master	//第一次推送
	git push origin master
17. 删除远程库
	git remote rm <name>	//解除本地和远程的绑定关系，并非物理上删除远程库
	git remote -v	//查看远程库信息

18. 克隆远程仓库	 git clone git@github.com:tianxin5750/learngit.git

19. 创建分支	git checkout -b fenzhi	//相当于 git branch fenzhi    git checkout fenzhi
		git branch	//列出所有分支，当前分支前有*号
		然后在当前分支上提交
		git checkout master	//切回主分支
		git merge fenzhi	//将fenzhi上的工作成果合并到master分支上
		git branch -d fenzhi	//删除fenzhi

20. switch	git switch -c fenzhi	//创建并切换到新的分支
		git switch master
