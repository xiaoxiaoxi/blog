# 写在前面

经常在本地把项目做的7788后再上传的服务器上，可能是一个不好的习惯把， 但是以前没Git呀，所以习惯了。整个操作过程也不天天做所以没有肌肉记忆，只有靠文字记录了



# 上传一个已有项目到Git服务器



## 准备工作

在服务器上创建一个项目， 然后将项目路径记录下来，我们设定为这个路径是 {remote repository}



## 客户端操作

1. 初始化本地仓库

   >  进入到当前客户端项目所在的根目录，输入命令初始化本地仓库
   >
   > git init

2. 设置忽略ignore规则

   > 在项目的根目录创建 .gitignore 文件，并设定规则，下面是java 常用的

   ~~~markdown
       ``` 配置文件
   *.class
   
   # Mobile Tools for Java (J2ME)
   .mtj.tmp/
   
   # Package Files #
   *.jar
   *.war
   *.ear
   
   # virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
   hs_err_pid*
   
   # 常用输出目录
   dist/
   target/
       ```
   ~~~

3. 添加所有资源

   > git add . 
   >
   > 将所有的资源加入

4. commit本地仓库

   > git commit -m’initial'
   >
   > 将加入的资源commit 到本地仓库，-m后面的message可以自己写，通常第一次我喜欢用这个

5. 设置远程仓库

   > git remote add origin {remote repository}
   >
   > 连接到远程仓库并为该仓库创建别名 , 别名为origin . 这个别名是自定义的，通常用origin

6. push代码到远程仓库

   > ##### git push -u origin master
   >
   > 创建一个 upStream （上传流），并将本地代码通过这个 upStream 推送到 别名为 origin 的仓库中的 master 分支上
   >
   > -u ，就是创建 upStream 上传流，如果没有这个上传流就无法将代码推送到 github；同时，这个 upStream 只需要在初次推送代码的时候创建，以后就不用创建了
   >
   > 