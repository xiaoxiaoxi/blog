# Git 常用操作基础

“Git跟踪并管理的是修改，而非文件。”——廖雪峰Git教程

GIT CHEAT SHEET presented by TOWER
生成一个新仓库
克隆一个已经存在的仓库 Clone an existing repository

## 本地操作 

> $ git clone ssh://user@domain.com/repo.git

生成一个新的本地仓库 Create a new local repository

> $ git init

本地仓库的操作
查看当前分支有哪些修改，掌握仓库当前的状态 Changed files in your working directory

$ git status
查看当前没有add的内容；查看修改了什么内容 Changes to tracked files

$ git diff FirstGit.c
把所有的文件修改添加到暂存区（Stage） Add all current changes to the next commit

$ git add .
将某文件中的改变添加到暂存区 Add some changes in <file> to the next commit

$ git add -p <file>
告诉Git，把文件提交到仓库，后附上本次提交的说明。实际上就是把暂存区的所有内容提交到当前分支

$ git commit -m "my first" 
提交所有本地的修改 Commit all local changes in tracked files

$ git commit -a
提交上一个阶段的修改 Commit previously staged changes

$ git commit
更改最后一次提交 Change the last commit Don‘t amend published commits!

$ git commit --amend
warning: LF will be replaced by CRLF in......
$ git config core.autocrlffalse
git提交时”warning: LF will be replaced by CRLF“提示

Please commit your changes or stash them before you merge.
git pull 之后发现有冲突，不管不顾的解决办法：放弃本地修改，直接覆盖之。

$ git reset --hard
$ git pull
入门
查看当前用户（global）配置

$ git config --global  --list  
设置名字与Email地址

$ git config --global user.name "Your Name" 
$ git config --global user.email "email@example.com"
一些常见的文件夹操作指令（新建文件夹、打开文件夹、显示当前位置、显示所有文件、显示含隐藏的所有文件）

$ mkdir learngit         
$ cd learngit
$ pwd
$ ls 
$ ls -a
一些常见文件操作指令（查看某个文件，删除某个文件）

$ cat readme.txt
$ rm test.txt
查看当前分支上面的日志信息；查看当前分支历史记录

$ git log
回退到上一个版本，或者回退到某个版本（commit id）

$ git reset --hard HEAD^
$ git reset --hard 1094adbxxxxxx
查看所有分支的所有操作记录（包括已经被删除的 commit 记录和 reset 的操作！）；查看命令历史

$ git reflog
丢弃工作区的修改: A.自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态 B.已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态

$ git checkout -- readme.txt
回退到当前HEAD版本（同时清暂存区）

$ git reset HEAD readme.txt
从版本库中删除一个文件

$ git rm test.txt
从版本库中删除一个文件夹

$ git rm -r build/
创建SSH Key

$ ssh-keygen -t rsa -C "youremail@example.com"
关联一个远程库

$ git remote add origin git@github.com:you/project.git
把本地库的内容推送到远程；把当前分支master推送到远程（第一条为首次，第二条为以后）

$ git push -u origin master
///
$ git push origin master
$ git push origin branch-name
克隆一个本地库

$ git remote add origin git@github.com:you/project.git
“Git鼓励你使用分支完成某个任务，合并后再删掉分支。”——廖雪峰Git教程

分支管理
创建并切换到dev分支

$ git checkout -b dev
仅创建分支，仅切换分支

$ git branch dev
$ git checkout dev
列出所有分支，并查看当前分支

$ git branch
切换回 master 分支

$ git checkout master
合并指定分支（敲入的）到当前分支

$ git merge dev
删除某个分支

$ git branch -d dev
强行删除某个分支

$ git branch -D dev
查看分支合并图（第一个是全部，第二个是简版）

$ git log --graph
///
$ git log --graph --pretty=oneline --abbrev-commit
合并指定分支到当前分支，创建一个新的commit，合并后的历史有分支，能看出来曾经做过合并

$ git merge --no-ff -m "Here is something" dev
把未完成的修改缓存到栈容器中；把当前工作现场“储藏”起来

$ git stash
查看所有的缓存

$ git stash list
恢复之前stash的版本

$ git stash apply 

$ git stash apply stash@{0}
删除stash的版本

$ git stash drop
恢复stash版本的同时把stash内容也删除

$ git stash pop
多人协作
查看远程库的信息

$ git remote -v
把该分支上的所有本地提交推送到远程库

$ git push origin master
创建远程origin的dev分支到本地，创建本地dev分支。这样即可时不时地把dev分支push到远程

$ git checkout -b dev origin/dev
$ git checkout -b branch-name origin/branch-name
更新代码；从远程抓取分支

$ git pull
设置dev和origin/dev的链接

$ git branch --set-upstream-to=origin/dev dev
$ git branch --set-upstream branch-name origin/branch-name
把本地未push的分叉提交历史整理成直线，使得我们在查看历史提交的变化时更容易

$ git rebase
标签管理
打一个新标签，注意默认是打在最新提交的commit上的

$ git tag v1.0
查看所有标签

$ git tag
针对某个commit id来打标签；追封一个标签

$ git tag v0.9 f52c633
查看标签信息

$ git show <tagname>
创建带有说明的标签，用-a指定标签名，-m指定说明文字

$ git tag -a <tagname> -m "blablabla..."
删除标签

$ git tag -d <tagname>
推送某个或全部标签到远程

$ git push origin <tagname>
/
$ git push origin --tags
从远程删除一个标签

$ git push origin :refs/tags/<tagname>
实战：如何在本地修改Github上的代码（前提要关联远程库）
1.从git上面把代码下载到本地

$ git clone https://github.com/Jiangxinghua/CANReflect.git

2.修改某些文件

3.提交修改到暂存区

$ git add main.c

4.提交到仓库

$ git commit -m "Modify in WorkPlace"
5.推送

$ git push

