# Git同时提交到多个远程仓库

2019-04-08阅读 1.4K0

使用git同时提交到多个远程库的操作方式为：

比如我需要你将同一份代码提交到如下的两个库中：

https://gitee.com/FelixBinCloud/recruit.git

https://git.coding.net/FelixBinCloud/recruit.git

（1）先添加第一个仓库：

```javascript
git remote add origin https://gitee.com/FelixBinCloud/recruit.git
```

（2）再添加第二个仓库： 

```javascript
git remote set-url --add https://git.coding.net/FelixBinCloud/recruit.git
```

如果还有其他，则可以像添加第二个一样继续添加其他仓库。

（3）然后使用下面命令提交： 

```javascript
git push origin --all
```

打开`.git/config`，可以看到这样的配置：

```javascript
[remote "origin"]
    url = https://gitee.com/FelixBinCloud/recruit.git
    fetch = +refs/heads/*:refs/remotes/origin/*
    url = https://git.coding.net/FelixBinCloud/recruit.git
```

刚才的命令其实就是添加了这些配置,也可以不用命令行，可以直接编辑该文件，添加对应的url即可。