![还发愁画流程图？IDEA这款神仙插件全部帮你搞定！](https://pic1.zhimg.com/v2-e807d63d950d8fcbfee1d1317a6b01c7_1440w.jpg?source=172ae18b)

# 还发愁画流程图？IDEA这款神仙插件全部帮你搞定！

[![老炮说Java](https://pica.zhimg.com/v2-42e984a13626fd46797b809f60b0af61_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/qing-chun-80-19)

[老炮说Java](https://www.zhihu.com/people/qing-chun-80-19)

3 人赞同了该文章

![img](https://pic1.zhimg.com/80/v2-327bc4c062f9ff192d2471421d14c9fc_1440w.jpg)

总有童鞋问，这个流程图图怎么绘制的，这个UML类图用什么工具做的等等，今天给大家推荐一款idea插件PlantUml，来帮助大家快速快速完成绘制。

## **PlantUml是什么**

PlantUml是一个支持快速绘制的开源项目。其定义了一套完整的语言用于实现UML关系图的描述，并基于强大的Graphviz图形渲染库进行UML图的生成。绘制的UML图还可以导出为图片,以及通用的矢量SVG格式文件。

## **PlantUML的优点**

- 完全文本方式编辑，无需控件拖拽，自动调节图元距离，简单美观
- 与开发平台完全无关，不受平台限制，只要有PlantUML jar包就能生成UML图
- 支持多种文本编辑器、ide的集成，例如idea、eclipse、notepad++等

作为一个Java coder，通常使用idea作为首选开发工具，我们以idea中的使用为主作介绍

## **idea安装 PlantUML插件**

File -> Settings -> Plugins 搜索 PlantUML ，找到 PlantUML integration 并安装

## **电脑安装graphviz**

下载地址

> [https://graphviz.gitlab.io/_pages/Download/windows/graphviz-2.38.msi](https://link.zhihu.com/?target=https%3A//graphviz.gitlab.io/_pages/Download/windows/graphviz-2.38.msi)

配置环境变量

首先添加一个变量名GRAPHVIZ_HOME, 变量值为安装路径 D:\WorkWare\Graphviz2.38 在Path目录下添加 `%GRAPHVIZ_HOME%\bin`, 多个配置之间要用 “;” 隔开 配置GRAPHVIZ_DOT, 变量值为 `%GRAPHVIZ_HOME%\bin\dot.exe`

![img](https://pic2.zhimg.com/80/v2-bf5b714e18682330ad74e561af2476e5_1440w.jpg)

> 横空出世，比Visio快10倍的画图工具来了。

![img](https://pic4.zhimg.com/80/v2-8c40728e1cb5bec043ee42508778ee67_1440w.jpg)

打开windows命令行, 使用dot -version出现以下页面就代表配置正常

![img](https://pic3.zhimg.com/80/v2-25ae8f10138e1e9e684073697d9badf2_1440w.jpg)

## **idea 配置graphviz**

File -> Settings -> Other Settings -> PlantUML

![img](https://pic3.zhimg.com/80/v2-02feb89cf42758888c5c3908989cc506_1440w.jpg)

## **使用plantUML画流程图**

新建uml 文件

![img](https://pic3.zhimg.com/80/v2-81def61fe86626c2da9eed2a1c85c73e_1440w.jpg)

输入测试文字

```text
@startuml  
Alice -> Bob: Authentication Request  
Bob --> Alice: Authentication Response  
  
Alice -> Bob: Another authentication Request  
Alice <-- Bob: another authentication Response  
@enduml  
```

右边会实时现实流程图

![img](https://pic2.zhimg.com/80/v2-835efeeb6df9e086ee502dca6245c985_1440w.jpg)

也可以根据所写的类，创建一个UML类图。也可以参考我们前天推荐的方式：IDEA中一个被低估的功能，一键把项目代码绘制成UML类图

![img](https://pic1.zhimg.com/80/v2-e3479c0119896efb40f4661df9121020_1440w.jpg)

## **其他**

如果不想装graphviz，想直接用，可以下载chrome插件PlantUML Viewer，安装之后直接编辑文本，可以在浏览器直接显示。

![img](https://pic3.zhimg.com/80/v2-30ce0ee5a040996956729f7940ba09aa_1440w.jpg)



发布于 2021-09-23 17:42





![基于JAVA源代码生成PlantUML类图](https://pic2.zhimg.com/v2-8a466ebf650f535d0c5cb3f308645c12_1440w.jpg?source=172ae18b)

# 基于JAVA源代码生成PlantUML类图

[![数字君](https://pic1.zhimg.com/v2-2564afda8db30800bb569ddd988899cb_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/shu-zi-jun-87-82)

[数字君](https://www.zhihu.com/people/shu-zi-jun-87-82)

程序员

10 人赞同了该文章

最近需要将一个项目逆向成类图，查找部分文档后发现IDEA的[UML类图](https://link.zhihu.com/?target=https%3A//www.jetbrains.com/help/idea/class-diagram.html)功能可以满足，使用后发现由于依赖关系过多，导致查看太混乱，无法突出重点。想到配合PlantUML integration插件手动编写类图，但是需要将源码中的类与相应的方法等粘贴出来，太过于浪费时间，于是想到借助源码解析器，通过程序将源码解析成PUML语法。

**PlantUML**是一个开源项目，支持快速绘制时序图、用例图、类图、活动图等，详情参考[PlantUML主页](https://link.zhihu.com/?target=https%3A//plantuml.com/zh/)。在IntelliJ中，可以使用[PlantUML integration](https://link.zhihu.com/?target=https%3A//plugins.jetbrains.com/plugin/7017-plantuml-integration) 或者 [markdown](https://link.zhihu.com/?target=https%3A//plugins.jetbrains.com/plugin/7793-markdown) 插件渲染PlantUML图形。

程序目前已经支持java文件解析和实现与继承关联功能，程序生成的文件符合PUML的标准语法，可以在任意支持PUML渲染的地方查看，并且可以根据需要，增加或者删除关系。详情参考开源地址:

[shuzijun/plantuml-parsergithub.com/shuzijun/plantuml-parser![img](https://pic4.zhimg.com/v2-df5fa8e12c4725a9e211adba204df4d7_ipico.jpg)](https://link.zhihu.com/?target=https%3A//github.com/shuzijun/plantuml-parser)

项目分为两部分:

1. plantuml-parser-core 解析的核心包，可以依赖此包在任意项目中进行解析，核心类为ParserConfig与ParserProgram ，依赖参考
2. plantuml-parser-plugin 借助核心包实现的IDEA插件，可以在项目中右键选择包或者类进行解析并生成类图

插件地址：

[PlantUML Parser - Plugins | JetBrainsplugins.jetbrains.com/plugin/15524-plantuml-parser![img](https://pic2.zhimg.com/v2-fd35b77052b6efdaffcc704514f92ee5_ipico.jpg)](https://link.zhihu.com/?target=https%3A//plugins.jetbrains.com/plugin/15524-plantuml-parser)

使用参考如下GIF:

![img](https://pic2.zhimg.com/v2-5e0c1e03009170f0ca1632c2e80a0e19_b.webp)





编辑于 2020-12-09 12:25