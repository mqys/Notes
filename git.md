* 生成key
```SHELL
ssh-keygen -t rsa -C "youremail@example.com"
```
* 设置用户名和email
```SHELL
git config --global user.name "your name"
git config --global user.email "youremail@example.com"
```
* creat a new repository and push to remote server
```SHELL
git init 
git add test.md
git commit -m "commite notes"
git remote add origin https://github.com/mqys/DestRepo
git push -u origin master
```
* 检查状态
```SHELL
git status
```
* 查看所关联的远程仓库的地址
```SHELL
git remote -v
```
* git关注的是文件的改动而不是文件本身，一次add是暂存一个版本，一次commit是提交一个版本。
* 查看项目历史
```SHELL
git log
```
可以通过使用参数来改变显示的样式
```
git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
```
详细内容查看`man git-log`
* 在$HOME目录下的.gitconfig文件中可以定义参数的别名
```
[alias]
co = checkout
hist = log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
```
* 获取旧版本，使用版本号的前7位hash值即可
```
git checkout <hash>
```
回到最新的版本
```
git checkout master
```
* 给当前版本打标签
```
git tag version1
```
使用`version1^`来表示version1的上一个版本，可以检出后给之前的版本打上标签，在checkout时可直接使用标签的名称
使用`git tag`来查看现存的标签
删除标签
```
git tag -d version1
```
* 撤销修改  
  * 撤销本地修改(add之前)
```
git checkout <filename>
```
  * 撤销暂存修改(add后，commit前)
```
git reset HEAD <filename> //重置暂存区内容
git checkout <filename>
```
  * 撤销提交修改(commit后)
```
git revert HEAD //撤回到上一个版本
```
  * 从分支撤销提交
```
git reset --hard <hash/tag> // --hard保持工作目录与新的分支一致
git hist --all //可以显示所有被打了标记的分支，包括被撤销的版本
```
* 修改文件内容，与上次提交合并成一次提交
```
git commit --amend -m "amend the previous commit"
```
* 移动文件
```
git mv <file> <DestDir> //改动后，仍然需要commit来提交修改
```
* 创建新的分支
```
git checkout -b <branch> 
//相当于git branch <branch name> 与 git checkout <branch name>
```
* 合并分支
```
git merge <branchname>
//若有冲突，则手动修复，再add commit
```
* 变基 rebase
```
git rebase <branchname> // 变基后将包含两个分支的全部修改，不建议使用
```
* clone repo
```
git clone <srcRepo> <desRepo>
```
* remote info
```
git remote   //show name of remote
git remote show <name> //show details of remote repo
```
* branches
```
git branch //show local branches
git branch -a //show all branches including remote branches
```
* get updates, not change
```
 git fetch
```
* merge updates
```
 git merge origin/master
```
* pull = fetch + merge
```
git pull // git fetch + git merge origin/master
```
* add local branch to track remote branch
```
git branch --track <localbranchname> origin/<remoteBranchName>
```
