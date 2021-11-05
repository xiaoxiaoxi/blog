# 写在前面

主要用Markdown来写Blog， 那就还是记录一下怎么使用Markdown吧，到时候也是方便一些。

一下搬运来自于 [菜鸟教程-Markdown](https://www.runoob.com/markdown/md-tutorial.html)



# Markdown 标题

Markdown 标题有两种格式。

### 1、使用 = 和 - 标记一级和二级标题

= 和 - 标记语法格式如下：

```
我展示的是一级标题
=================

我展示的是二级标题
-----------------
```

显示效果如下图：

![img](https://www.runoob.com/wp-content/uploads/2019/03/01986C87-7E19-4497-878E-AE996AFC088E.jpg)

### 使用 # 号标记

使用 **#** 号可表示 1-6 级标题，一级标题对应一个 **#** 号，二级标题对应两个 **#** 号，以此类推。

```
# 一级标题
## 二级标题
### 三级标题
#### 四级标题
##### 五级标题
###### 六级标题
```

显示效果如下图：

![img](https://www.runoob.com/wp-content/uploads/2019/03/md2.gif)



# Markdown 段落

Markdown 段落没有特殊的格式，直接编写文字就好，**段落的换行是使用两个以上空格加上回车**。

![img](https://www.runoob.com/wp-content/uploads/2019/03/36A89BDA-A062-4D66-A41B-0EBEE7891AB9.jpg)

当然也可以在段落后面使用一个空行来表示重新开始一个段落。

![img](https://www.runoob.com/wp-content/uploads/2019/03/3F254936-778E-417A-BEF2-467116A55D00.jpg)

------

## 字体

Markdown 可以使用以下几种字体：

```
*斜体文本*
_斜体文本_
**粗体文本**
__粗体文本__
***粗斜体文本***
___粗斜体文本___
```

显示效果如下所示：

![img](https://www.runoob.com/wp-content/uploads/2019/03/md3.gif)

------

## 分隔线

你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

```
***

* * *

*****

- - -

----------
```

显示效果如下所示：

![img](https://www.runoob.com/wp-content/uploads/2019/03/3F46EAA9-DADE-48FD-99AA-DF7BEBFAA4FA.jpg)

------

## 删除线

如果段落上的文字要添加删除线，只需要在文字的两端加上两个波浪线 **~~** 即可，实例如下：

```
RUNOOB.COM
GOOGLE.COM
~~BAIDU.COM~~
```

显示效果如下所示：

![img](https://www.runoob.com/wp-content/uploads/2019/03/B5270A31-15D0-410B-AE1D-B9655B8F331C.jpg)

------

## 下划线

下划线可以通过 HTML 的 **<u>** 标签来实现：

```
<u>带下划线文本</u>
```

显示效果如下所示：

![img](https://www.runoob.com/wp-content/uploads/2019/03/05A27273-B66D-43DE-A3DB-0D32FF024093.jpg)

------

## 脚注

脚注是对文本的补充说明。

Markdown 脚注的格式如下:

```
[^要注明的文本]
```

以下实例演示了脚注的用法：

```
创建脚注格式类似这样 [^RUNOOB]。

[^RUNOOB]: 菜鸟教程 -- 学的不仅是技术，更是梦想！！！
```

演示效果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/md5.gif)

# Markdown 列表

Markdown 支持有序列表和无序列表。

无序列表使用星号(*****)、加号(**+**)或是减号(**-**)作为列表标记，这些标记后面要添加一个空格，然后再填写内容：

```
* 第一项
* 第二项
* 第三项

+ 第一项
+ 第二项
+ 第三项


- 第一项
- 第二项
- 第三项
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/89446A8E-6D83-4666-AACC-980145D5F070.jpg)

有序列表使用数字并加上 **.** 号来表示，如：

```
1. 第一项
2. 第二项
3. 第三项
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/560384BB-2B00-41D5-ACF2-18972F7F2775.jpg)

### 列表嵌套

列表嵌套只需在子列表中的选项前面添加四个空格即可：

```
1. 第一项：
    - 第一项嵌套的第一个元素
    - 第一项嵌套的第二个元素
2. 第二项：
    - 第二项嵌套的第一个元素
    - 第二项嵌套的第二个元素
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/8ED795DA-F124-4E70-BA71-57CD9CF958A4.jpg)

# Markdown 区块

Markdown 区块引用是在段落开头使用 **>** 符号 ，然后后面紧跟一个**空格**符号：

```
> 区块引用
> 菜鸟教程
> 学的不仅是技术更是梦想
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/DFE1124E-BC38-4C12-B7AC-053E560D4C9C.jpg)

另外区块是可以嵌套的，一个 **>** 符号是最外层，两个 **>** 符号是第一层嵌套，以此类推：

```
> 最外层
> > 第一层嵌套
> > > 第二层嵌套
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/AA0A4A6A-33A7-48C7-971F-73FFC8FE85B0.jpg)

### 区块中使用列表

区块中使用列表实例如下：

```
> 区块中使用列表
> 1. 第一项
> 2. 第二项
> + 第一项
> + 第二项
> + 第三项
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/E3BF6399-6483-4C7A-8502-AE75E8D66C96.jpg)

### 列表中使用区块

如果要在列表项目内放进区块，那么就需要在 **>** 前添加四个空格的缩进。

列表中使用区块实例如下：

```
* 第一项
    > 菜鸟教程
    > 学的不仅是技术更是梦想
* 第二项
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/1B894FB4-53AC-4E2D-BA30-F4AE4DFA8B97.jpg)

# Markdown 代码

如果是段落上的一个函数或片段的代码可以用反引号把它包起来（**`**），例如：

```
`printf()` 函数
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/C928FDA3-E0A7-4AFF-AB2A-B3AF44F93DF9.jpg)

### 代码区块

代码区块使用 **4 个空格**或者一个**制表符（Tab 键）**。

实例如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/55EDFE05-5F27-458E-AFE0-7B96685C9603.jpg)

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/6DC89E5C-B41A-4938-97D8-D7D06B879F91.jpg)

你也可以用 **```** 包裹一段代码，并指定一种语言（也可以不指定）：

````
```javascript
$(document).ready(function () {
    alert('RUNOOB');
});
```
````

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/88F52386-2F98-4D7E-8935-E43BECA6D868.jpg)

# Markdown 链接

链接使用方法如下：

```
[链接名称](链接地址)

或者

<链接地址>
```

例如：

```
这是一个链接 [菜鸟教程](https://www.runoob.com)
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/49E6CB42-F780-4DA6-8290-DC757B51FB9A.jpg)

直接使用链接地址：

```
<https://www.runoob.com>
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/9BFF60A1-DD71-4B63-987B-4665B31C7787.jpg)

### 高级链接

我们可以通过变量来设置一个链接，变量赋值在文档末尾进行：

```
这个链接用 1 作为网址变量 [Google][1]
这个链接用 runoob 作为网址变量 [Runoob][runoob]
然后在文档的结尾为变量赋值（网址）

  [1]: http://www.google.com/
  [runoob]: http://www.runoob.com/
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/EC3ED5D2-4F0D-492A-81B3-D485623D1A9E.jpg)

# Markdown 图片

Markdown 图片语法格式如下：

```
![alt 属性文本](图片地址)

![alt 属性文本](图片地址 "可选标题")
```

- 开头一个感叹号 !
- 接着一个方括号，里面放上图片的替代文字
- 接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上选择性的 'title' 属性的文字。

使用实例：

```
![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png)

![RUNOOB 图标](http://static.runoob.com/images/runoob-logo.png "RUNOOB")
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/A042DF30-C232-46F3-8436-7D6C35351BBD.jpg)

当然，你也可以像网址那样对图片网址使用变量:

```
这个链接用 1 作为网址变量 [RUNOOB][1].
然后在文档的结尾为变量赋值（网址）

[1]: http://static.runoob.com/images/runoob-logo.png
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/75AA6EBF-CC57-44A6-A585-5EE3DD94E42A.jpg)

Markdown 还没有办法指定图片的高度与宽度，如果你需要的话，你可以使用普通的 <img> 标签。

```
<img src="http://static.runoob.com/images/runoob-logo.png" width="50%">
```

显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/55F2A67D-F4BD-4960-AC55-DC690A415878.jpg)

# Markdown 表格

Markdown 制作表格使用 **|** 来分隔不同的单元格，使用 **-** 来分隔表头和其他行。

语法格式如下：

```
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

以上代码显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/23EACC50-38E0-4284-B99A-6BC22E284BAC.jpg)



对齐方式

**我们可以设置表格的对齐方式：**

- **-:** 设置内容和标题栏居右对齐。
- **:-** 设置内容和标题栏居左对齐。
- **:-:** 设置内容和标题栏居中对齐。

实例如下：

```
| 左对齐 | 右对齐 | 居中对齐 |
| :-----| ----: | :----: |
| 单元格 | 单元格 | 单元格 |
| 单元格 | 单元格 | 单元格 |
```

以上代码显示结果如下：

![img](https://www.runoob.com/wp-content/uploads/2019/03/87DE9D5C-44FB-4693-8735-194D3779EC3E.jpg)

# Markdown 高级技巧

### 支持的 HTML 元素

不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。

目前支持的 HTML 元素有：`<kbd> <b> <i> <em> <sup> <sub> <br>`等 ，如：

```
使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑
```

输出结果为：

![img](https://www.runoob.com/wp-content/uploads/2019/03/81999271-F914-428D-B7BF-164BDC67CAAC.jpg)

### 转义

Markdown 使用了很多特殊符号来表示特定的意义，如果需要显示特定的符号则需要使用转义字符，Markdown 使用反斜杠转义特殊字符：

```
**文本加粗** 
\*\* 正常显示星号 \*\*
```

输出结果为：

![img](https://www.runoob.com/wp-content/uploads/2019/03/CA0E0162-0C48-41CD-B57A-CB32A4287C02.jpg)

Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

```
\   反斜线
`   反引号
*   星号
_   下划线
{}  花括号
[]  方括号
()  小括号
#   井字号
+   加号
-   减号
.   英文句点
!   感叹号
```

### 公式

当你需要在编辑器中插入数学公式时，可以使用两个美元符 $$ 包裹 TeX 或 LaTeX 格式的数学公式来实现。提交后，问答和文章页会根据需要加载 Mathjax 对数学公式进行渲染。如：

```
$$
\mathbf{V}_1 \times \mathbf{V}_2 =  \begin{vmatrix} 
\mathbf{i} & \mathbf{j} & \mathbf{k} \\
\frac{\partial X}{\partial u} &  \frac{\partial Y}{\partial u} & 0 \\
\frac{\partial X}{\partial v} &  \frac{\partial Y}{\partial v} & 0 \\
\end{vmatrix}
${$tep1}{\style{visibility:hidden}{(x+1)(x+1)}}
$$
```

输出结果为：

![img](https://www.runoob.com/wp-content/uploads/2019/03/1061D800-D44C-436D-A1EA-1CBDA95A5209.jpg)

 [Markdown 表格](https://www.runoob.com/markdown/md-table.html)

## 1 篇笔记 写笔记

1. 

     adc

    928***528@qq.com

    [ 参考地址](https://jingyan.baidu.com/article/48b558e3035d9a7f38c09aeb.html)

   849

   ### typora 画流程图、时序图(顺序图)、甘特图

   复制以下代码使用 typora 的源码模式粘贴到编辑器中查看效果：

   ![img](https://www.runoob.com/wp-content/uploads/2019/03/22A9BC11-BA3E-40D8-90B0-DC4FD29F9C02.jpg)

   以下几个实例效果图如下：

   **1、横向流程图源码格式：**

   ````
   ```mermaid
   graph LR
   A[方形] -->B(圆角)
       B --> C{条件a}
       C -->|a=1| D[结果1]
       C -->|a=2| E[结果2]
       F[横向流程图]
   ```
   ````

   **2、竖向流程图源码格式：**

   ````
   ```mermaid
   graph TD
   A[方形] --> B(圆角)
       B --> C{条件a}
       C --> |a=1| D[结果1]
       C --> |a=2| E[结果2]
       F[竖向流程图]
   ```
   ````

   **3、标准流程图源码格式：**

   ````
   ```flow
   st=>start: 开始框
   op=>operation: 处理框
   cond=>condition: 判断框(是或否?)
   sub1=>subroutine: 子流程
   io=>inputoutput: 输入输出框
   e=>end: 结束框
   st->op->cond
   cond(yes)->io->e
   cond(no)->sub1(right)->op
   ```
   ````

   **4、标准流程图源码格式（横向）：**

   ````
   ```flow
   st=>start: 开始框
   op=>operation: 处理框
   cond=>condition: 判断框(是或否?)
   sub1=>subroutine: 子流程
   io=>inputoutput: 输入输出框
   e=>end: 结束框
   st(right)->op(right)->cond
   cond(yes)->io(bottom)->e
   cond(no)->sub1(right)->op
   ```
   ````

   **5、UML时序图源码样例：**

   ````
   ```sequence
   对象A->对象B: 对象B你好吗?（请求）
   Note right of 对象B: 对象B的描述
   Note left of 对象A: 对象A的描述(提示)
   对象B-->对象A: 我很好(响应)
   对象A->对象B: 你真的好吗？
   ```
   ````

   **6、UML时序图源码复杂样例：**

   ````
   ```sequence
   Title: 标题：复杂使用
   对象A->对象B: 对象B你好吗?（请求）
   Note right of 对象B: 对象B的描述
   Note left of 对象A: 对象A的描述(提示)
   对象B-->对象A: 我很好(响应)
   对象B->小三: 你好吗
   小三-->>对象A: 对象B找我了
   对象A->对象B: 你真的好吗？
   Note over 小三,对象B: 我们是朋友
   participant C
   Note right of C: 没人陪我玩
   ```
   ````

   **7、UML标准时序图样例：**

   ````
   ```mermaid
   %% 时序图例子,-> 直线，-->虚线，->>实线箭头
     sequenceDiagram
       participant 张三
       participant 李四
       张三->王五: 王五你好吗？
       loop 健康检查
           王五->王五: 与疾病战斗
       end
       Note right of 王五: 合理 食物 <br/>看医生...
       李四-->>张三: 很好!
       王五->李四: 你怎么样?
       李四-->王五: 很好!
   ```
   ````

   **8、甘特图样例：**

   ````
   ```mermaid
   %% 语法示例
           gantt
           dateFormat  YYYY-MM-DD
           title 软件开发甘特图
           section 设计
           需求                      :done,    des1, 2014-01-06,2014-01-08
           原型                      :active,  des2, 2014-01-09, 3d
           UI设计                     :         des3, after des2, 5d
       未来任务                     :         des4, after des3, 5d
           section 开发
           学习准备理解需求                      :crit, done, 2014-01-06,24h
           设计框架                             :crit, done, after des2, 2d
           开发                                 :crit, active, 3d
           未来任务                              :crit, 5d
           耍                                   :2d
           section 测试
           功能测试                              :active, a1, after des3, 3d
           压力测试                               :after a1  , 20h
           测试报告                               : 48h
   ```
   ````

   效果图如下：

   ![img](https://www.runoob.com/wp-content/uploads/2019/03/md-flow.png)

   [adc](https://www.runoob.com/note/47651)  adc 928***528@qq.com [ 参考地址](https://jingyan.baidu.com/article/48b558e3035d9a7f38c09aeb.html)2年前 (2019-10-18)