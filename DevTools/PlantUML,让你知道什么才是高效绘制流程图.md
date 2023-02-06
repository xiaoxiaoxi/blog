![PlantUML,让你知道什么才是高效绘制流程图](https://pic2.zhimg.com/v2-156413105e9523bc432733ab99570776_1440w.jpg?source=172ae18b)

# PlantUML,让你知道什么才是高效绘制流程图

[![bobocode](https://pic1.zhimg.com/v2-24d8d786baaf43c4fd3ec71cccc39bb0_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/bobo_code)

[bobocode](https://www.zhihu.com/people/bobo_code)

全栈工程师

51 人赞同了该文章

## **官方网址**

[开源工具，使用简单的文字描述画UML图。plantuml.com/zh/index](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/index)

## **PlantUML是一个开源项目，支持快速绘制的类型：**

[顺序图的语法和功能plantuml.com/zh/sequence-diagram![img](https://pic1.zhimg.com/v2-94aa6a0689d021a73cb7ba3adbbf6990_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/sequence-diagram)

[用例图语法和功能plantuml.com/zh/use-case-diagram![img](https://pic1.zhimg.com/v2-3276dee587f9e50610d0455c7c8da968_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/use-case-diagram)

[类图的语法和功能plantuml.com/zh/class-diagram![img](https://pic3.zhimg.com/v2-a2b1458b9e4ef008287942d0a0582052_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/class-diagram)

[新的活动图测试语法和功能plantuml.com/zh/activity-diagram-beta![img](https://pic4.zhimg.com/v2-11880c41ea6e468a332fcfb7a2eac997_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/activity-diagram-beta)

[组件图的语法和功能plantuml.com/zh/component-diagram![img](https://pic2.zhimg.com/v2-816e9bc24a7c9e4077df33554b0689d1_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/component-diagram)

[状态图的语法和功能plantuml.com/zh/state-diagram![img](https://pic2.zhimg.com/v2-f2282d4f3c9147f6e0806e090bc6ce2d_ipico.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/state-diagram)

[对象图plantuml.com/zh/object-diagram](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/object-diagram)

[部署图plantuml.com/zh/deployment-diagram](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/deployment-diagram)

[时序图的语法和特性plantuml.com/zh/timing-diagram![img](https://pic1.zhimg.com/v2-213f09172b6e86d5b7fe4c746cf9a30c_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/timing-diagram)

## **同时还支持以下非UML图:**

[绘制盐GUI样机plantuml.com/zh/salt![img](https://pic2.zhimg.com/v2-215a0113ce619e828bd6e9666942e529_ipico.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/salt)

[Archimate Supportplantuml.com/zh/archimate-diagram![img](https://pic1.zhimg.com/v2-e30102f87e3579c25ae5b380c9ac64fc_ipico.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/archimate-diagram)

[新的活动图测试语法和功能plantuml.com/zh/activity-diagram-beta#sdl![img](https://pic4.zhimg.com/v2-11880c41ea6e468a332fcfb7a2eac997_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/activity-diagram-beta%23sdl)

[Integration of Ditaaplantuml.com/zh/ditaa![img](https://pic1.zhimg.com/v2-06a5890249ac9a88824f11621e9859c0_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/ditaa)

[甘特图plantuml.com/zh/gantt-diagram](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/gantt-diagram)

[思维导图plantuml.com/zh/mindmap-diagram](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/mindmap-diagram)

[WBS work breakdown structure syntax and featuresplantuml.com/zh/wbs-diagram![img](https://pic3.zhimg.com/v2-3d2b9697bc51151f6e6656e2ee42b76e_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/wbs-diagram)

[复杂公式的 Ascii Math 语法plantuml.com/zh/ascii-math![img](https://pic3.zhimg.com/v2-85d86316e69d863c8731035aa9234892_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/ascii-math)

[Entity Relationship diagram syntax and featuresplantuml.com/zh/ie-diagram![img](https://pic3.zhimg.com/v2-786b0ecee97f1140d80c40265fa890f6_180x120.jpg)](https://link.zhihu.com/?target=http%3A//plantuml.com/zh/ie-diagram)

## **本地绘图**

[Download plantuml from SourceForge.netsourceforge.net/projects/plantuml/files/plantuml.jar/download](https://link.zhihu.com/?target=http%3A//sourceforge.net/projects/plantuml/files/plantuml.jar/download)

1. 新建文件`sequenceDiagram.txt`

\2. 写入

```todotxt
@startuml
Alice -> Bob: test
@enduml
```

\3. 运行

```
java -jar plantuml.jar sequenceDiagram.txt
```

会在本地成sequenceDiagram.png的图片

![img](https://pic1.zhimg.com/80/v2-8a5cfd64e5e2a6d0b69e6edcce3d2fb0_720w.png)

## **安装 chrome 插件 PlantUML Viewer**

![img](https://pic3.zhimg.com/80/v2-b39c711ecd91c4792952e821564f2cfa_720w.jpg)

1. 把文件sequenceDiagram.txt 拖到chrome 浏览器

**遇到的问题 文件没有解析** 不起作用的原因是没开启允许访问文件网址

![img](https://pic2.zhimg.com/80/v2-588d3ce84d08780c8f2e0bc69db56f4d_720w.jpg)

\2. 开启允许访问文件网址

![img](https://pic2.zhimg.com/80/v2-b9adf884fea2534704012e26d9ecb265_720w.png)

![img](https://pic3.zhimg.com/80/v2-787371b63af179a2b12c7b9ae4cc0586_720w.jpg)

## **workpress 插件 PlantUML Renderer的使用**

![img](https://pic2.zhimg.com/80/v2-e1c6272adac0a0fbde1149863c10e375_720w.png)

```text
[plantuml] 
Alice -> Bob: Authentication Request 
Bob --> Alice: Authentication Response
Alice -> Bob: Another authentication 
Request Alice <-- Bob: another authentication Response 
[/plantuml]
```

![img](https://pic4.zhimg.com/80/v2-87ff1ee69ee18b6d5213ecb88eca3797_720w.jpg)

发布于 2019-08-06 20:09