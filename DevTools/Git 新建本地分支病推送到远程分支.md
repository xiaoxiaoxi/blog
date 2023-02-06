# Git新建本地分支并推到远程分支

## 进入
cd 进入远程项目代码所在的本地路径(例如：远程项目名Test，本地存放路径：E:\Demo\Test) 注意：斜杠

> `` cd E:/Demo/Test ``

## 新建本地分支

``` git checkout -b t ```

> 注意：  
> git checkout命令加上-b参数表示创建并切换，相当于以下两条命令

```
$ git branch t
$ git checkout t
```

> 注：
> 1. 也可以远程新建分支然后拉到本地(例如：远程分支是demo)  
```git checkout -b demo origin/demo    //检出远程的demo分支到本地```
> 2. 切换分支  
``` git checkout master  //切换到demo分支 ```

## 查看所有分支

查看所有本地仓库分支和远程分支
``` git branch -al ```

> 注：
> 1. 前面带有remotes的分支都是远程分支。
> 2. 星号(*)表示当前所在分支。
>

## 提交本地分支到远程分支

``` git push origin t:t ```

## 删除分支

```git push origin --delete  demo //删除远程分支 demo ```


> 注：   
> 也可以直接推送一个空分支到远程分支，起始就相当于删除远程分支：  
```git push origin :demo  //推送本地的空分支(冒号前面的分支)到远程origin的demo(冒号后面的分支)(没有会自动创建) ```

