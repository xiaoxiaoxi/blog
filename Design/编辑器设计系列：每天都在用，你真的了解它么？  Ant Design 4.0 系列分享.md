![编辑器设计系列：每天都在用，你真的了解它么？ | Ant Design 4.0 系列分享](https://pica.zhimg.com/v2-68863eade3e202e44caa9fbb35207944_1440w.jpg?source=172ae18b)

# 编辑器设计系列：每天都在用，你真的了解它么？ | Ant Design 4.0 系列分享

[![Eleven幺幺](https://pic3.zhimg.com/v2-c4465d341cb4081e7af131327a10f03b_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/yang-ying-89-56)

[Eleven幺幺](https://www.zhihu.com/people/yang-ying-89-56)[](https://www.zhihu.com/question/48510028)

蚂蚁集团 体验设计专家

146 人赞同了该文章

提起编辑器，你会想到什么？

也许你从来没有意识到，但是从接触计算机开始，你就和各种编辑器打上了交道。

Windows 98 中的画图软件也许是你的启蒙。计算机课上当你敲下第一个五彩斑斓的字，作出第一张会动的幻灯片，画出第一个图表，Office 三件套开启了一扇新的大门。再后来，你学会了用记事本写下第一行 if…else…， 但始终没能学会怎么用 PS 修图，不过幸好很快学会了用美图秀秀。现在的你，可能在各行各业，你的电脑上装满各种专业软件，每天一打开它们，可能一天就过去了。你依赖着这些专业软件完成工作赚钱养家，如果哪天它们不小心崩了，丢失了辛苦一天的成果，你大概可以问候遍所有它的亲戚。

百年以前，人们的生产工具还都是实实在在看得见摸得着的物品。可现在，就在一方小屏幕中，通过各种各样的虚拟工具，尤其是其中的编辑器，你的生产力得到了翻天覆地的提升。生产力工具的好用与否，直接关系到每个人的工作和生活。

这，就是编辑器设计的意义所在。

我第一份工作是为年纪比我还大的工程届软件老大哥 AutoCAD 进行设计，后来去了创业公司做智能设计工具 Arkie。再后来加入蚂蚁金服体验技术部，机缘巧合成为语雀的设计师。不知不觉这几年一路走来都和编辑器设计“杠上了“，现在终于有机会好好向大家介绍我这位“老朋友”。

## 主流的编辑器类型

按照编辑器的可视化程度，我们可以把市面上的编辑器大致分为以下三类：

1. **可视化编辑器（Nocode）**
   根据 [WYSIWYG](https://link.zhihu.com/?target=http%3A//ui-patterns.com/patterns/WYSIWYG%3Fdeer_tracert_token%3De37f9126-5241-4de4-aeb0-6c81a51cbd84) （What You See is What You Get）设计模式为没有代码或 Markup 语言基础的用户提供的一种所见即所得编辑器。这也是我们日常生活中接触最多的编辑器类型。
2. **源代码类编辑器（Procode）**
   主要指通过编程语言编写计算机程序的应用程序。它一般包括代码编辑器、编译器、调试器和图形用户界面等工具。各领域的专业研发同学应该最为熟悉它。
3. **源代码与可视化相结合编辑器（Lowcode）**
   上述两种编辑方式的混合体。兼有可视化编辑器的易操作性，又有源代码类编辑器的高灵活度。



按照编辑器平台分类，又可以分为以下三类：

1. **桌面客户端编辑器**
   早期很多编辑器都是为专业人士提供，满足其多样化的专业生产要求，提高生产效率。因此在专业场景下，桌面端软件是编辑器的常用载体。
2. **Web 编辑器**
   随着互联网技术发展，富 Web 应用的诞生使得在线上模拟桌面端软件成为可能。相比于桌面端，Web 编辑器可以随时随地访问，无需下载安装，适合多人协作。这些特性帮助编辑器将其目标人群进一步扩大为所有普通用户，以满足普罗大众的通用性需求。
3. **移动端编辑器**
   进入移动互联网时代后，移动端办公成为常态，不管是专业用户还是普通用户，都有移动端使用需求。编辑器又进一步为适应移动端衍化。通常移动端版本编辑器只保留最基础功能，更侧重查看分享。但是图像、视频类编辑器有所不同，因为移动端就是生产端，所以直接在移动端编辑的场景应运而生，出现了非常多优秀的移动端图像、视频类编辑器。 移动端编辑器主要指各种原生应用中的编辑器，但是移动端网页的编辑器模式也可以参照此类。

## 用户在编辑器中的行为

要想研究编辑器设计，还得先从研究人入手。

相比于其他产品，编辑器中的功能数量往往更多，因为在编辑器中用户有时需要完成复杂工作。通过分析用户在编辑器中的行为，可以帮助我们了解用户可以在编辑器完成什么工作，进而清晰了解编辑器需要具备什么功能。

《界面设计模式》一书中介绍过，人类在进行创造性工作时，往往不是一蹴而就，而是不断通过「创造-调整-再创造」多次循环往复完成，这样的模式称之为递增构建（Incremental Instruction）。如果在这个过程中工具可以及时响应用户行为，那么用户就更容易全身心投入到创造中，达到心流状态（Flow）。

据此，可以将用户在编辑器中的工作流程抽象为4步：

**第一步：输入**
用户在编辑器中添加对象，比如 x, y, z…

输入的方式主要有如下几种：

- 按最小颗粒度添加，比如一个文字，一个图形，一个图片……
- 按封装好的区块添加，比如一个包含文字图片的广告素材
- 按模板添加，比如一张表格模板
- 从已有对象开始，比如已经写了一半的文档

**第二步：调整**
对上一步输入的对象进行修改。这个阶段主要会有几类操作：

- 对全局执行一个命令（Command，即指是为了完成某种特定任务而向程序发送的指示），比如最常见的命令保存、撤销、重做。
- 对单个对象执行一个命令，比如复制、剪切和粘贴。
- 直接改变全局的属性（Attribute），比如设置文档的纸张大小。
- 直接改变单个对象的属性。比如改变文字的大小、颜色。

通过这一步，原来的(x, y, z)就变为了(ax, by, cz)

**第三步：查看**
在调整完后，对自创作进行审视，检查其是否符合目标。此时往往需要借助工具以便更好地查看审阅对象的完成度。比如放大缩小画布，隐藏某些内容等。

**第四步：输出**
在确认创建的对象符合自己的预期后，用户就可以输出对象进行后续操作，比如发布、导出、分享…

在这一步中，(ax, by, cz)被打包输出为f(x, y, z)。

所以用户在编辑器中的行为其实就是 ![[公式]](https://www.zhihu.com/equation?tex=+f%28x%2C+y%2C+z%29%3Dax%2Bby%2Bcz+) 的过程。

据此，我们也就明晰了一个编辑器中需要具备的主要功能，分别是：输入类功能、调整类功能、查看类功能和输出类功能。

## 编辑器的常见界面模块

上述梳理出的 4 大类功能，每一类都需要在编辑器中有相应界面承载。下面就介绍编辑器中常见的界面模块。一个模块有时会为多类功能服务，但各自有所侧重。

## 画布

《界面设计模式》中称之为中央舞台 （Center Stage），现在更常见称为画布（Canvas）。主要用于放置执行一系列操作后的结果，比如代码片段、文档、表格、图片等。同时被操作对象的常用功能也可直接在画布内执行，比如移动、缩放、旋转。

![img](https://pic1.zhimg.com/80/v2-d63075a913b3e806dbe49fdbb1637378_1440w.jpg)编辑器中的图片自带调整尺寸大小的手柄，方便就地操作

## 菜单

按照位置和出现方式，可以分为固定菜单栏（Menubar）和情境菜单（Contextual Menu）。固定菜单栏在桌面端编辑器中非常常见，承载了编辑器中的所有功能。在部分 Web 编辑器也会使用固定菜单栏，但只保留基础功能的 Web 编辑器则更多使用情境菜单。

**固定菜单栏（Menubar）**

主要位于编辑器顶部，所有功能都会在这里进行高密度组织和隐藏，不占太多空间。非常适合喜欢探索的新手用户在这里发现更多功能。

![img](https://pic2.zhimg.com/80/v2-7f8a1113d9808ed760ce4f00942fd495_1440w.jpg)



**情境菜单（Contextual Menu）**

在需要时才会出现，主要通过当前的选择或点击显示相关命令，方便就地操作。右键菜单就是典型代表，菜单中可以承载所有对当前选择对象可执行的功能。

此外，情景菜单也可以承载输入类功能：通过点击画布中的加号出现情景菜单，从菜单里选择一个对象，然后插入到编辑器中。

![img](https://pic3.zhimg.com/v2-b55b1af096af6b3ec2bb87b2e3398fba_b.jpg)



为了适应不同对象的展示需求，如今的菜单早已不局限于文字，还可以图形化展示。Microsoft UWP 设计体系中建议可以为重要的或者语义明确的菜单项添加图标，但不必为了追求一致而加上一些语义不明的图标，反而会增加视觉干扰，分散用户注意力。

菜单的排列方式除了单列，也可以多列，只要能方便用户快速识别和检索的。 总体上越来越趋向于下文将提到的浮动面板。

![img](https://pic4.zhimg.com/v2-6afd62394c98acc6fa28b0cd217c9783_b.jpg)





菜单中可以进行的操作，也不再局限于选择，还可以进行属性设置，显示辅助信息。

![img](https://pic2.zhimg.com/80/v2-874d384596bbeb31fc3ba5a9381cc471_1440w.jpg)带有开关按钮、辅助信息的菜单

## 工具栏

工具栏也可以分为固定工具栏（Toolbar）和情境工具栏（Contextual Toolbar）。

在桌面端编辑器中，菜单栏是用户学习了解编辑器所有功能的好地方，而Web 编辑器并不都配备菜单栏，用户会更加依赖固定工具栏探索编辑器功能。

但如果编辑器足够简单，则有时连固定工具栏都可以省略，通过情境工具栏或情境菜单反而更加方便编辑。

**固定工具栏（Toolbar）**

一般位于编辑器顶部，在图形类编辑器中也经常看到位于左侧的工具栏。当输入类型比较简单时，可以将入口放在工具栏，比如添加形状、文本框等。常用的全局性操作也会放置于工具栏，比如放大缩小工具。

![img](https://pic3.zhimg.com/80/v2-84b0bc96367491aef7f8f096a9e471c2_1440w.jpg)

当对象的属性数量较少，则修改属性的功能也会放置在工具栏上。所有功能根据按相关性分组，展现形式也不局限于图标，还可以是输入框、下拉选择器等。

![img](https://pic2.zhimg.com/80/v2-63fc04f06707aef1e8a599e2baf45bc5_1440w.jpg)

Microsoft UWP 设计体系中提到，工具栏有纯图标、图标+标签两种展现形式。当空间充足时，可以显示图标+标签，标签通常位于图标底部如果空间进一步充足，标签可以位于图标右侧。当用户希望沉浸式工作时，也可以隐藏工具栏，依靠快捷键操作。 工具栏中各个功能的合理布局很重要，可以帮助用户快速找到合适工具。可以按照功能性质、使用频率分组。值得注意得时，对于有从左到右阅读习惯的用户，并不是最左功能就最容易被发现，反而是画布中心上方位置更容易引起用户注意。

**情境工具栏（Contextual toolbar）**

当用户与某个对象交互时才会出现，通常可以对该对象的执行调整命令，或修改对象属性。

![img](https://pic4.zhimg.com/v2-8af9fe8094fed2d7654d0b0f8ec04577_b.jpg)



在实际设计中，情境工具栏经常和情境菜单可以结合使用。前者直接展示主要命令，而将辅助命令折叠到「…」的情境菜单中。

![img](https://pic1.zhimg.com/80/v2-faa9c3eecc97d7bc2bb5d32fa81823d8_1440w.jpg)

##  工具板

工具板（Tool Palette）与工具栏类似，出现时间早于工具栏，通常放置在左侧。MacPaint 可能是是最早应用工具板的软件，也正因此后来很多各类图形编辑器也采用了这种交互，甚至影响了后来图形编辑器的工具栏位置。 典型代表就是 Adobe Photoshop、Illustrator 左侧两列图标按钮。

![img](https://pic2.zhimg.com/80/v2-68ec773e2827fdbc23c261ec36c7d011_1440w.jpg)

与工具栏不同的是，工具板上会承载输入类和调整类功能，但不会展示目标对象的属性。下面是《About Face 4》中对于工具栏和工具板区别的介绍：

> 工具栏是一系列立即可以访问的命令组合，只有选中某个命令，该命令才能发挥作用，而且这些命令通常都和改变对象的属性有关。而工具板包含的是一些列互斥的功能，有且只有一个功能处于激活状态，每个功能包含了一个操作状态：对象创建状态、对象选择状态、对象操作状态。

怎么理解上面这段话呢？举个例子，比如 Photoshop 中，你选中套索工具后，当下只能使用这个工具，并且还会出现一个配套的工具栏，展示更多具体设置帮助操作，但如果此时想要使用吸管工具，你必须重新在工具板中选择，这就是所谓的一些列互斥功能。但是工具栏上的命令相对更简单，选中命令然后执行即可，比如 Sketch 中，从工具栏添加矩形，然后可以继续其他操作，比如选择、旋转、移动，合并路径，而无需切换到领个状态才能进行下一步，这样的操作效率也会高很多。

值得注意的是，在 Adobe 的最新设计语言 Spectrum 中已经没有这个模块，而是由左侧工具栏结合图标按钮代替实现。

## 面板

面板主要用于取代原来经常使用的对话框。对话框属于模态设计，在编辑器中过多使用对话框，会造成用户注意力不断被跳出的对话框所打断，降低工作效率，所以面板这种非模态形式应运而生，因为用户与面板进行交互时，可以随时切换到其他模块进行观察或操作，对于高效工作很有帮助。[Salesforce 的 Lightening 设计语言](https://link.zhihu.com/?target=https%3A//lightningdesignsystem.com/guidelines/builder/%3Fdeer_tracert_token%3D464a39df-1b25-42cb-bd3b-e43834101a8b%23site-main-content)中明确对比了面板和对话框的各自优劣处：

**面板**

- 优点： 小到中型的面板主要放置一些关于编辑器的上下文内容。通栏面板适合查看单个典型元素和其他大量的视觉元素。
- 缺点：部分或完全遮挡画布，不要有「新增、读取、更新、删除」的操作，否则可能让人困惑。

**对话框**

- 优点：可以简单地放一些「保存」，「取消」，类似于「新增、读取、更新、删除」这样的操作。应用场合更广泛。通过隐藏其他内容，可以帮助用户更好的聚焦当前对话框。
- 缺点：完全遮挡了画布。难以同时参考画布或工具栏上的其他内容。

根据所占面积大小，可以分为固定面板和浮动面板。

**固定面板（Panel）**

通常出现在编辑器两侧或底部，可以包含一些常驻控件，也可以根据选择而改变控件。根据承载的功能，又可以进一步分为以下3类：

**索引类：**通过文字或缩略图，方便用户快速查看特定部分内容。

![img](https://pic4.zhimg.com/80/v2-1d8bdf74ec95fd1be7baafe96337a1d3_1440w.jpg)文档编辑器中的大纲

![img](https://pic3.zhimg.com/80/v2-079b6b7d103bb8a0dfad4eb60fd0ea0e_1440w.jpg)多媒体编辑器中的缩略图导航

**输入类**：当需要从模板等复杂对象开始创建时，通常会将它们展示在左侧面板。在实际设计中，如何权衡面板的信息展示效率和面板占用整个编辑器界面的比例是个值得研究的话题。

![img](https://pic4.zhimg.com/80/v2-d523b82155f1de46ba2ffb5ad2bd3ca7_1440w.jpg)左侧面板提供了非常多模板选择

属性类：当全局或单个对象属性数量很多，工具栏无法承载时，可以用右侧面板承载

![img](https://pic2.zhimg.com/80/v2-fac84a4c8d6cc756f855513c23107539_1440w.jpg)右侧面板展示了对长队可以设置的属性

**浮动面板**

浮动面板的用户基本和固定面板一致。主要当内容较少，不足以占满整个浏览器高度时，可以选择浮动面板，以减少占用编辑器空间。



**![img](https://pic4.zhimg.com/80/v2-dd57852abda15eecd09ac9a0acd2d097_1440w.jpg)索引类：导航地图**



![img](https://pic3.zhimg.com/80/v2-b43498dbd6c1ea988a654a9da81fed5a_1440w.jpg)索引类：查找和替换

![img](https://pic1.zhimg.com/80/v2-bc6a27adccca89370b06637f05155aac_1440w.jpg)属性类：设置形状属性

## Ribbon

Ribbon 是微软在 Office 2007 中引入的一个新模块，本质是带有标签的菜单栏和工具栏混合体。 这个设计模式的引入主要是因为当时 Office 产品遇到的一些困境：新功能越来越多，但很少有用户发现并使用这些功能。随之而来软件变得越来越复杂，体验一年不如一年，操作效率也越来越低。在这样的困扰下，微软投入 3 年时间来了一次设计大变革， Ribbon 设计模式诞生了。

![img](https://pic4.zhimg.com/80/v2-059786e38086111b2d0ed3ff35209353_1440w.jpg)

更多Ribbon背后前世今生的故事，可以阅读下文。

[梓义：设计考古(1)_工具类产品 Office275 赞同 · 37 评论文章![img](https://pic1.zhimg.com/v2-dc6171ab64e2c40467fc06e5e44bd82c_180x120.jpg)](https://zhuanlan.zhihu.com/p/90304083)

如今大多数 Web 编辑器通常都只保留桌面端编辑器20%的主要功能，加上情境工具栏和情境菜单的帮助，所以比较少使用 Ribbon。但是电子表格编辑器可能是个例外，因为其命令非常多，即使是 Web 编辑器，一个工具栏的空间也不太足够，加上它的各种命令仅用一个图标有时候也不是很直观，配上文字后，对空间的需求更大了。

![img](https://pic3.zhimg.com/80/v2-18b3fb25ddf80ca93337237b4ff1927e_1440w.jpg)



## 为不同需求而设计

和绝大多数工具型产品一样，编辑器的用户也可以根据其经验程度分为：新手用户、中级用户和专家用户。 以下为《About Face 4：交互设计精髓》中对于三者的解释。

![img](https://pic3.zhimg.com/80/v2-dddf9bc1ffec8e6dc6ca4ddc58d183ae_1440w.jpg)

书中也指明了设计需要更多地为中级用户设计，因为新手和专家始终是少数，随着时间的推移两者也慢慢会变成中级用户。所以相应的设计目标是：

- 迅速轻松地将新手培养成中级用户。
- 不要在中级用户成长为专家用户的过程中设置障碍。
- 最重要的是，保证永久的中级用户在技术范围的中段探索时又愉悦的体验。

## 提供多种命令模态

《About Face 4》中提到了为不同经验程度用户而设计的命令模态（Command Modality）。 前面提到过命令就是为了完成某种特定任务而向应用程序发送的指示。而命令模态是让用户将这些指令发给应用的特殊技术，例如直接操作柄（direct-manipulation handle）、下拉菜单、工具栏控件以及快捷键等。具体可以分为以下三类命令模态。

- **教学式命令**
  特点它们往往包含描述性文本教会用户如何使用，比如对话框和菜单。这些命令可能用户原先并不知道，但是它稳定地存在与现实中，只要用户寻找就发现，所以可以很好的帮助喜欢探索的新手用户。
- **直接命令**
  可以让命令直接生效，而不需要中间步骤，比如拖放处理，实时反馈的控件。当新用户逐渐成长后中级用户后，教学式命令那种缓慢、重复、冗长的过程就会令人乏味，所以用户会寻找更多直接命令来完成常用任务。
- **隐形命令**
  通常在界面上没有或只有少许关于它们的提示。快捷键、手势操作。这些命令要求用户记忆，一旦记住了就会很易用，所以专家用户偏爱这类命令。

所以为了满足不同经验的用户需求，在编辑器中同一个功能有时会重复提供以上几种命令模态。

那么到底哪些功能适合有多种命令模态呢？功能使用的频率来是判断标准之一。

书中将中级用户最常用的功能定义为有效功能工作集（working set）。设计师可以事先定义一个最小有效工作集，这些功能默认都会包含多种命令模态。当这样也无法满足用户的需求时，可以允许用户把自己其他常用的命令也加到这个有效工作集中，以满足不同用户的不同工作习惯。

虽然是编辑器中一个功能往往会有多个命令模态，但是有一个例外，就是比较危险的命令，比如放弃修改，清除等，不应该有那么轻易操作的方式，相反最好在菜单或对话框中呆着。

在实际使用中，用户容易发现教学式命令，但直接命令和隐藏命令可能并不容易被发现，所以需要通过一些途径告知用户它们的存在。这些方法被称之为记忆矢量。最差劲的记忆矢量就是在帮助文档中提到它们，因为这个要求用户能够主动去寻找。 稍好一点的做法是把记忆矢量集成到编辑器的主界面：

1. **利用空置状态**

![img](https://pic4.zhimg.com/80/v2-0e715047dc9f9a6f24027bb0b404c133_1440w.jpg)

**2. 利用等待时间**

![img](https://pic3.zhimg.com/80/v2-6c0bb6c6261226719cfafb3bc1846016_1440w.jpg)



**3. 搭建工具栏和菜单栏的记忆矢量**

在菜单中加入与工具栏一样的图标以建立关联。

![img](https://pic1.zhimg.com/80/v2-d6cc2784061588610c2641b1c4bb62cc_1440w.jpg)



直接放到菜单栏中、tooltip中。

![img](https://pic3.zhimg.com/80/v2-0c3a6cd52b520267fd92f36a87991226_1440w.jpg)

![img](https://pic1.zhimg.com/80/v2-dc077774fe0a7c355d087630d1d7fb98_1440w.png)



**4. 搭建界面功能的热键的提示**

热键（mnemonie）是微软定义的一种快捷操作。 如下图，在 Office Word 中按住 Alt 键，顶部功能区就会出现提示符号（数字或者字母），然后根据提示继续在键盘上输入，就相当于用鼠标点击选择了某个功能，界面上会出现一批新的提示符号，以进行下一步操作。通过这种方式，用户可以通过键盘完成大部分操作。

![img](https://pic1.zhimg.com/80/v2-89cac7acadd0c207c535e5b0ec3d592c_1440w.jpg)

![img](https://pic1.zhimg.com/80/v2-713ac419bb9d2e8fcea4811b7bd12758_1440w.jpg)

## 自定义配置

不同用户会有不同喜好，而用户的喜好有可能是截然相反的。所以必须提前定义清晰编辑器的目标用户到底以哪类人群为主，是否要兼顾有不同喜好的不同群体。如果答案是肯定的，那么就需要提供自定义配置来满足不同用户的需求。 专家用户往往会有更多的自定义配置需求，而大部分用户可能在很长一段时间内都只会使用默认配置。所以设计师必须选择一个符合更大多数人的默认选项。

![img](https://pic1.zhimg.com/80/v2-a8887a7eec9d8b3e97a1a0833b03ea98_1440w.jpg)

![img](https://pic1.zhimg.com/80/v2-106f25e61865a681c75cbd0d1608a10c_1440w.jpg)

## 不能忽略的键盘设计

在编辑器中用户往往需要长时间工作，而键盘的输入效率高于鼠标点选，所以用户（尤其是专家用户）对键盘的依赖很大（进行文字输入、导航和触发操作）。这也就要求设计师需要考虑到键盘的使用方式。

Microsoft UWP 介绍了键盘设计的如下相关建议。

### Tab 键和方向键

Tab 键可以用于界面中控件之间导航（Shift + Tab 可以反向导航），让用户逐个激活界面中的控件，以进行输入、选择等操作，而无需切换去用鼠标激活。 而方向键通常用于某个控件的内部导航，比如可以用上下键调整输入框中的数值。

![img](https://pic3.zhimg.com/80/v2-e6bcf84c588de628888fb3d6ea117692_1440w.jpg)

**Enter 键**

在非文字输入的时候，Enter 键可执行多种常见的用户交互：

1. 当前界面中主按钮的快捷方式，比如确认、提交、完成等。
2. 激活当前控件，比如激活输入框、下拉菜单。

![img](https://pic4.zhimg.com/80/v2-145e5e05f4e8b02a0d39ba3465376af7_1440w.jpg)

### 空格键

在非文字输入的时候，空格键可以调用与聚焦的控件关联的操作或命令（类似于点按触摸屏或用鼠标单击）。虽然 Enter 键和 Space 键并不总是执行相同的操作，但经常是执行相同操作。

![img](https://pic3.zhimg.com/80/v2-6d6f10bc3da97980f48169bb8530663a_1440w.jpg)

### Esc 键

Esc 键让用户可以退出临时性的界面和操作，比如：

1. 界面中的「取消」「关闭」「退出」按钮的快捷方式。
2. 退出当前控件的激活态。

![img](https://pic3.zhimg.com/80/v2-36d4bec19493cdf292a6e85047b19f96_1440w.jpg)

### 快捷键

快捷键也是提高编辑器中工作效率的一大方式，对于专家用户尤为重要。 [Apple Human Guidline Interface ](https://link.zhihu.com/?target=https%3A//developer.apple.com/design/human-interface-guidelines/macos/user-interaction/keyboard/%3Fdeer_tracert_token%3D464a39df-1b25-42cb-bd3b-e43834101a8b)中提到两条快捷键的设计原则：

- 遵守标准快捷键，这样才有利于用户将在别处习得的知识无缝衔接到当前编辑器。
- 为常用操作创建快捷键。如果这还不能满足用户，需要考虑提供自定义快捷键的方式。

具体更多快捷键设计技巧可以参考以下文章：

[苏文苑：⌨️快捷键的体验设计24 赞同 · 0 评论文章![img](https://pic2.zhimg.com/v2-772ec5a989ab794f69ed9af542540845_180x120.jpg)](https://zhuanlan.zhihu.com/p/113663697)

------

洋洋洒洒写了好长一篇关于编辑器的研究报告，感谢你能看到这里，同时也感谢蚂蚁金服体验技术部的另两位设计师舒宇和瀚雅的贡献，共同完善本报告。

编辑器设计真是一个古老又冷门的领域。欢迎移步语雀，查看更多编辑器设计系列文章

[编辑器设计系列：每天都在用，你真的了解它么？ · 语雀www.yuque.com/elevenyang/tvy47l/qdugkw![img](https://pic1.zhimg.com/v2-9cbc2fec5a8380bdf2272fcce49ed7e8_180x120.jpg)](https://link.zhihu.com/?target=https%3A//www.yuque.com/elevenyang/tvy47l/qdugkw)



> 小彩蛋：《界面设计模式》是这份研究报告的参考书之一，在2008年出版了第一版，当我发现其中有一个章节专门介绍编辑器时感觉如获至宝，后来发现在2013年又出了第二版，正当我兴致勃勃想去看看新版本中关于编辑器部分的更新时，万万没想到作者把编辑器整章删除了……



## 参考资料

[Microsoft Fluent Design System](https://link.zhihu.com/?target=https%3A//www.microsoft.com/design/fluent/%23/windows)
[Adobe Spectrum Design Language](https://link.zhihu.com/?target=https%3A//spectrum.adobe.com/)
[Apple Human Interface Guidelines](https://link.zhihu.com/?target=https%3A//developer.apple.com/design/human-interface-guidelines/)
[Salesforce Lightening Design System](https://link.zhihu.com/?target=https%3A//lightningdesignsystem.com/guidelines/builder/%23site-main-content)
[SAP Fiori Design Guidelines](https://link.zhihu.com/?target=https%3A//experience.sap.com/fiori-design-web/toolbar-overview/)
[《About Face 4：交互设计精髓》](https://link.zhihu.com/?target=https%3A//book.douban.com/subject/26642302/%3Fdeer_tracert_token%3D464a39df-1b25-42cb-bd3b-e43834101a8b)
[《设计考古(1)_工具类产品 Office》](https://link.zhihu.com/?target=https%3A//www.yuque.com/ant-design/ant-design/kff9g2%3Fdeer_tracert_token%3D464a39df-1b25-42cb-bd3b-e43834101a8b%237Oze2)
[《Web 界面设计》](https://link.zhihu.com/?target=https%3A//book.douban.com/subject/3821157/)
[《界面设计模式》（第1版 & 第2版）](https://link.zhihu.com/?target=https%3A//book.douban.com/subject/25716088/)
[《Web 导航设计》](https://link.zhihu.com/?target=https%3A//book.douban.com/subject/3313897/)

编辑于 2020-04-15 19:48