# Godot3游戏引擎入门之零零：简单的想法

[![刘庆文](https://pic2.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

32 人赞同了该文章

## 一、缘由

今年 7 月份，也就是上个月，惊奇的发现世界上存在着这么一个小巧灵动的游戏引擎：[Godot Game Engine](https://link.zhihu.com/?target=https%3A//godotengine.org/) ，图标非常可爱另类，研究了一番，现在已经是 3.0 的版本（目前是 3.0.6 ），看官方新闻，最新版 3.1 正在紧张有序的开发中，据说会有重大突破，期待。 :joy:

这个游戏引擎虽小，但是真的是五脏俱全：支持 Window/Mac/Linux 主流操作系统，支持普通的 2D 和 3D 游戏开发，支持 Android/iOS/Blackberry OS 等主流手机平台，以及 XBox/Steam/GameRoom 等其他游戏平台的发布，当然 WebGL 也不在话下。你可以到[官方网站](https://link.zhihu.com/?target=https%3A//godotengine.org/download)下载直接运行文件， Mac 也可以通过 `brew cask install godot`安装，最大不超过 100M ，最低 20M ，但功能可谓是非常齐全啊。

![img](https://pic1.zhimg.com/80/v2-3ed2ed15134db0139cc8e54fd87f9488_720w.jpg)Godot 3 开源游戏引擎

令人惊喜的是，他是开源的！开源的，没错，你没有听错，早在四年前就已经开源了，哇哦~不过，不好意思，四年前我连如日中天的 Unity3D 是啥都不知道呢。去年底有机会接触并学习了一段时间的 Unity3D 游戏开发后，还是蛮喜欢这个游戏开发引擎的，但是现在我发现作为游戏开发爱好者菜鸟的我， Godot 更适合我，为啥？请听我慢慢道来：

1. 小巧开源，社区驱动，下载后无需安装，开箱即用，官方插件也齐全
2. 惊喜的 2D 游戏开发界面和 GUI 元素，适合新手，打开程序即可轻松上手游戏开发
3. 一切基于 Node ，想添加任何元素都是极其 Easy ，甚至 2D 和 3D 以及 GUI 元素混用都没关系
4. 每一个 Node 元素**只能添加一个** Script 脚本进行控制，这太符合是我这类有一点点 Adobe Flash 开发经验的朋友了
5. 如果深入点，它的流程设计，帮助文档，资源加载，一切可以基于场景进行设计，等等，都非常直接、非常贴切啊~~~

当然，学习曲线平缓也是我喜欢这个游戏引擎的另一个重要原因。这就是我接触 Godot 没超过两周的感受吧，当然还有更多更多的优点等着去挖掘和探索的，官方对此也列举了 Godot 平台的几乎所有的特性及优点，大家可以在此查看： [Godot Features](https://link.zhihu.com/?target=https%3A//godotengine.org/features)

总之，就是这么一个五脏俱全、小巧玲珑的开源的游戏开发引擎让我爱不释手，我决定“冒天下之大不韪”对 Godot 进行个人方面的努力宣传尝试，为开源界也算是贡献我的一份渺小的力量吧。哈哈。 :joy:

## 二、内容

因为自己对游戏开发也几乎是完全从 0 开始，目前有没有入门都还处于不确定阶段，我肯定不能进行一些深入的探讨，但是基础的部分我会边学习边记录下来，作为小专题来和喜欢 Godot 的朋友们一起讨论研究。

关于内容的话，我初步给自己定了一个目标，找了些资料和书籍，主要基于 2D 游戏开发，参考了《 Godot Engine Game Development in 24 Hours, Sams Teach Yourself: The Official Guide to Godot 3.0 》这本书后，我把内容简单的列表如下：

1. Godot 游戏引擎的介绍和安装、以及相关的资源
2. Godot 的场景系统介绍和使用
3. 2D 图形相关元素和操作
4. GDScript 脚本介绍和使用
5. 用户输入 Input 相关
6. 游戏物理引擎
7. 动画的使用
8. 简单的开发流程探讨
9. 文件系统和项目管理
10. 声音和粒子系统
11. 视口和 GUI 界面元素
12. 网络相关
13. 最后可能会探讨一下 Native 脚本吧
14. 其他……

好吧，这真是画了一个好大的饼啊……希望自己跪着也能吃完吧，哈哈。 :joy:

## 三、其他

啰嗦了一大堆，大家肯定会问：凭什么要上船呢？特别是很多朋友可能有其他游戏引擎的开发经验，比如国内如火如荼的 [Unity 3D](https://link.zhihu.com/?target=https%3A//unity3d.com/) ，还有大名鼎鼎的老资格 [Unreal Engine](https://link.zhihu.com/?target=https%3A//unigine.com/)，以及游戏画面闻名的 [Cry Engine](https://link.zhihu.com/?target=https%3A//www.cryengine.com/) 等等，还有手机上著名的 [SpriteKit](https://link.zhihu.com/?target=https%3A//developer.apple.com/documentation/spritekit) 框架，以及开源跨平台的 [LibGDX](https://link.zhihu.com/?target=https%3A//libgdx.badlogicgames.com/) 或者 [Cocos2d-x](https://link.zhihu.com/?target=http%3A//www.cocos2d-x.org/) 游戏框架经验，等等，话说最近开源的 [Xenko](https://link.zhihu.com/?target=https%3A//xenko.com/)又是个什么梗？我想说，凭我的软文还不够大家上船，那么先来两篇文章安利一下大家吧：

- 这里有一位国外大“屌”开发者，谈了他对 Godot 和自己多年 Unity3D 游戏开发经验的一些比较和看法，我觉得蛮有参照价值的，参考网址：

> Here is my personal opinion about Godot vs Unity[https://news.ycombinator.com/item?id=16674933](https://link.zhihu.com/?target=https%3A//news.ycombinator.com/item%3Fid%3D16674933)）：

- 还有一个位大神，在去年底 Medium 上发了一篇文章，也是关于为什么选择 Godot 的原因，原文太长了，参考网址：

> Why we choose Godot Engine[https://medium.com/@rockmilkgames/why-godot-engine-e0d4736d6eb0](https://link.zhihu.com/?target=https%3A//medium.com/%40rockmilkgames/why-godot-engine-e0d4736d6eb0)

我感觉自己要翻译一下这两篇文章了，因为阅读这些英文有点浪费时间，我也并没有足够的说服力来让大家趟坑 Godot ，哈哈。那么，可能下篇见吧。 :sunglasses:



# Godot3游戏引擎入门之一：熟悉编辑器界面

[![刘庆文](https://pica.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

41 人赞同了该文章

## 一、前言

Godot 3.1 第一个 Alpha 预览版本已经发布，预览版所有的新特性都已敲定，激动人心，就等着稳定的正式版了！大家可以去官网一探究竟：[DEV SNAPSHOT: GODOT 3.1 ALPHA 1](https://link.zhihu.com/?target=https%3A//godotengine.org/article/dev-snapshot-godot-3-1-alpha-1) 。

> 本篇内容： Godot 入门之编辑器相关介绍阅读时间： 5 分钟永久链接：[http://liuqingwen.me/blog/2018/09/03/introduction-of-godot-3-part-1-the-editor/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/09/03/introduction-of-godot-3-part-1-the-editor/)

## 二、正文

## 关于下载

Godot 非常小，我下载的 64 位 Windows 版本总大小不到 40M ，官网下载页面直达：[https://godotengine.org/download](https://link.zhihu.com/?target=https%3A//godotengine.org/download) ，下载 zip 包后解压无需安装，直接使用，不过这里有三件小事情我要告诉大家：

1. 下载对应的版本还有发布模板： Godot 支持多个操作系统，注意对应的系统以及架构（ 32 位或者 64 位操作系统），然后就是发布模板（ Export Templates ），这个在下载页面的下方可以找到，当然刚开始使用 Godot 玩玩的时候是没必要下载的，当你需要发布最终产品到 Windows/Mac/iOS/Android 等平台的时候你再下载也不迟，后面的文章我应该会提到模板使用。
2. 配置文件夹位置：如果你直接打开 **Godot.exe** ，那么它的配置文件默认生成在 C 盘目录下（我使用的是 Win10 系统），但是你可以随时改回来，只需要在 Godot 软件文件夹下创建一个 `_sc_` 的文件即可，后面我有截图说明。
3. 分辨率设置：如果你和我一样使用的是 4K 高分显示屏幕，那么你在打开 Godot 编辑器后需要进一步设置，这个现在提出来，等会介绍编辑器的时候我有截图作具体介绍。

另外，在官网你会发现一个名为： *MONO VERSION (C# SUPPORT)* 的下载链接，这个是支持使用 C# 语言来进行游戏编程的，我没怎么使用，看官方介绍，我的建议是没必要下载这个版本，一方面它需要 MONO 的支持，而且 C# 支持现在还不是特别稳定（够用级别吧），另一方面，我觉得 Godot 的脚本语言 **GDScript** 非常简单，比 Python 还简单没压力，后续文章我会专门介绍。

![img](https://pic1.zhimg.com/80/v2-a429f6070fbe3d087469d2dded1b7f2c_720w.jpg)Godot files

OK ，双击 exe 文件，开始那愉快的 Godot 之旅吧，骚年！ :sunglasses:

OK ，双击 exe 文件，开始那愉快的 Godot 之旅吧，骚年！ :sunglasses:

## 界面介绍

**首先是开场白**

打开 Godot 第一眼是很普通的项目控制面板，这里可以设置编辑器的显示语言：

![img](https://pic4.zhimg.com/80/v2-9783baf0ec29088058b3d2f12a265757_720w.jpg)godot_1_startup_window.jpg

选择创建一个游戏，或者打开已存在的游戏，也可以下载官方的 Demo ，双击进入编辑器主界面：

![img](https://pic1.zhimg.com/80/v2-6939322bc89babcb293803c6f56b4ce8_720w.jpg)godot_1_editor_main.jpg

Godot 的主界面很普通，用过 Unity 或者类似工具软件的朋友都不会感觉到陌生。 Godot 默认打开的是 3D 场景，可以通过上方的菜单进行切换，我推荐使用快捷键： *2D场景 -> F1 ， 3D 场景 -> F2 ， Script 脚本窗口 -> F3 ， Help 搜索帮助 -> F4* 。

**开工前设置**

如果你打开 Godot 窗口，发现字体很小，那很正常，因为我们没有设置过字体大小，可以在*编辑器 -> 编辑器设置*菜单下进行设置：

![img](https://pic2.zhimg.com/80/v2-1f7229991f4c52a959fc1e625c7af1c9_720w.jpg)godot_1_settings_editor.jpg

另外，如果是 4K 高分辨率屏幕，当你迫不及待地添加一个 Node 节点，然后保存，运行，选择刚才保存的场景，游戏开始，你会发现你的窗口不会出现在屏幕的正中央位置，而是右下方，看起来很不舒服，这是因为你没有开启 HIDPI 设置，别急，只需要在*项目 -> 项目设置*里设置就可以了：

![img](https://pic4.zhimg.com/80/v2-53a559c21ea979a7eae8e5286862fc2f_720w.jpg)godot_1_settings_project.jpg

勾选 HiDPI 然后运行你的游戏，就会显示在屏幕正中央了，如果不是 4K 高分屏这一步没必要。

**节点和场景**

在尝试运行游戏之前，你得创建一个*入场*场景，然后保存，接着设置为启动场景才能正常运行。添加节点非常简单，在节点窗口上方有个 **+** 号，点击它，或者直接快捷键更方便： *CTRL + A* ，会弹出很多预制节点供您选择：

![img](https://pic2.zhimg.com/80/v2-1cc23b47459a40beb8e07df727e4bdcd_720w.jpg)godot_1_node_1.jpg

注意， *Node* 是所有节点的父节点，你可以使用它来作为场景的根节点（ Root ），因为它既是 2D 节点的父节点，又是 3D 节点的父节点，所以你甚至可以使用 *Node* 来混合 2D 和 3D 游戏节点！当然，我更建议直接使用相对应的节点： *Node2D* 表示所有 2D 节点的父节点， *Spatial* 为所有 3D 节点父节点，而 *Control* 为所有控件的父节点。

除此之外，你会发现，他们都有一套自己的颜色，比如 2D 节点图标是淡蓝色， 3D 节点是粉红色，控件则为绿色，还有一个，深入一点你就会发现，很多 2D 节点名字都对应一个 3D 节点，下面列举几个：

3D 节点2D 节点节点名CameraCamera2D相机LightLight2D灯光ParticlesParticles2D粒子AreaArea2D碰撞区域KinematicBodyKinematicBody2D物理学物体StaticBodyStaticBody静态物体RigidBodyRigidBody2D刚体CollisionShapeCollisionShape2D碰撞体形状PathPath2D路径

如上图，你还可以直接通过搜索，更加方便的添加你所需要的节点。在 Godot 中一切基于节点，甚至 *Timer* 都是一个节点，所以它必须添加到节点树中才能正常使用，这些后续会提到。

**属性面板和子菜单**

我添加了一个 *Node2D* 作为场景的根节点，单击命名为 `Game` ，然后在 `Game` 根节点下添加一个子节点，可以直接 *CTRL + A* 来添加，这里我是直接把资源窗口中的 Logo 图片直接拖拽到了场景中，选择 *Sprite* 创建一个精灵：

![img](https://pic4.zhimg.com/80/v2-91f120aff6bb7432a9ca75ae2c04324f_720w.jpg)godot_1_add_sprite.jpg

这个时候，右边场景中就会自动创建一个 *Sprite* 节点，选中这个节点，右下角就是这个节点对应的属性面板，你会发现， *Sprite* 的 `Texture` 属性已经自动设置为刚才拖拽的那张 logo 图片了。同时，你会发现在场景的下方多了一个菜单项： *Texture Region* 材质区域的编辑区，这就是对应该节点的底部栏操作面板，在后续的文章中，介绍动画的时候会经常用到这里的编辑区和菜单。

![img](https://pic1.zhimg.com/80/v2-b65218f3f73f8cfca072d18db7db6dbc_720w.jpg)godot_1_bottom_part.jpg

如图，注意场景上方，额外有些子菜单可以进行操作，这些子菜单非常重要，后续对很多节点都会使用到，我这里列举几个类型节点对应的子菜单，如图：

![img](https://pic3.zhimg.com/80/v2-bbb19798704235fffd04570e6cd7614a_720w.jpg)godot_1_sub_menu_1.jpg

![img](https://pic1.zhimg.com/80/v2-500a647dde7461064e1a4a53f4f69ac0_720w.jpg)godot_1_sub_menu_3.jpg

![img](https://pic3.zhimg.com/80/v2-f524b623e91e0896996bb3c3bd106986_720w.jpg)godot_1_sub_menu_2.jpg

软件界面大概就这些了，常用的功能都应该差不多介绍到位了吧。 :smile:

## 编程语言

在本系列的第一篇文章中，我说过如果你曾经是 Adobe Flash 的开发者，那么你对 Godot 中**一个节点绑定一个脚本**的约定会感觉非常熟悉。选择一个节点，在上方的右上角，一个带 **+** 号的书本按钮，点击便可以给相应节点添加脚本：

![img](https://pic4.zhimg.com/80/v2-8b1b71ba13cfa5eecb596adf99dabe6b_720w.jpg)godot_1_add_script.jpg

注意：在打开的脚本编辑器里，也有对应的**脚本菜单**。另外， Godot 非常贴心的一点是，你随时可以按 F4 呼出帮助，然后搜索你想要了解的 API ，查看相关属性和方法，这对新手来说，简单不要太爽啊！

![img](https://pic2.zhimg.com/80/v2-e6941040fde0162430e3f0dc257c6815_720w.jpg)godot_1_sub_menu_4.jpg

![img](https://pic3.zhimg.com/80/v2-698a1b3e57401be5f08dbdb02531e496_720w.jpg)godot_1_search_api_1.jpg

关于脚本语言编程和使用，这个是一个很长的话题了，暂且到此吧，不过我觉得只要有点编程基础的朋友在 GDScript 脚本上是很容易上手的。后续我必须出个专门的文章，专门介绍一下 GDScript 脚本吧。

## 三、其他

这次就说到这里，大家感觉这个**游戏**怎样？“什么？什么游戏？”哈哈，偷偷告诉你， Godot 编辑器本身也是由 Godot 引擎打造的一个游戏： [Godot's Engine is a Godot Game itself!](https://link.zhihu.com/?target=https%3A//github.com/godotengine/godot/issues/4181%23issuecomment-203516916) ，惊不惊喜，意不意外？ :sunglasses:



# Godot3游戏引擎入门之二：第一个简单的游戏场景

[![刘庆文](https://pica.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

24 人赞同了该文章

## 一、前言

最近工作时间安排地非常紧凑，除了周日一天，已经没有其他空闲时间了。不过到了 10 月份会慢慢恢复，目前我在抽出一点时间好好准备这个 [Godot 系列](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)，边写边学习边迎接[Godot 3.1 版本](https://link.zhihu.com/?target=https%3A//godotengine.org/)的到来，也算是一件高兴地事情，哈哈。 :sunglasses:

> 主要内容： Godot 2D 小游戏入门之场景和节点创
> 阅读时间： 6-8 分
> 永久链接：[http://liuqingwen.me/blog/2018/09/11/introduction-of-godot-3-part-2-game-scene-and-node/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/09/11/introduction-of-godot-3-part-2-game-scene-and-node/)

## 二、正文

## 本篇目标

1. 学习场景的创建和基本设置，游戏的运行，第一个小 Demo
2. 了解几个基本节点的相关功能：`Node2D/Sprite/RigidBody2D/CollisionShape2D/`
3. 丰富我们的小游戏场景，学习静态物体和刚体碰撞以及 Debug 功能

## 创建场景

我们的目标是在 Godot 中创建一个物理小世界，做个碰撞小测试。相关的图片资源和最终项目我会上传到 [Github](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos) ，算是第一个小 Demo 吧。 :smile:

第一步：首先是进行一个视窗设置，游戏最终窗口大小。*在菜单栏 -> Project -> Project Settings -> General* 下，选择 *Display -> Window -> Size* 下设置宽度和高度，如果找不到设置选项可以点击搜索，我这里设置的是 *600 x 1000* ，根据自己的需求随意设定，另外我们还可以设置游戏的视口（ viewport ），这里暂时不设置，后续文章我再详谈。

第二步：如果你现在急着运行的话， Godot 会提示你没有选择初始场景入口，所以我们先要在场景中创建一个主节点。在节点窗口添加一个根节点，你可以选择 *Node* ，也可以选择 *Node2D* ，甚至其他节点都没关系。还记得上一篇我介绍过的吗？ *Node* 是 2D 和 3D 节点的共同父节点，所以 2D 游戏场景中使用 *Node* 作为父节点没任何问题。我这里选择的是 *Node2D* ，接着单击命名为 *Game* ，保存场景为 `Game.tscn` ，然后按 *F5*运行，选择刚保存的 *Game* 场景作为游戏启动入口，确定运行。

第三步：在上一步完成后游戏运行我们知道啥都没有是因为场景中只有一个空的根节点。是时候添加一些游戏元素了，这就是 Godot 中丰富的节点体系。我们要做一个自由落体小 Demo 。简单描绘一下：有一个地面作为静态物体，做一个球体从空中自由落下，观察碰撞情形。非常非常简单，是不是？如何在 Godot 中实现呢？有两种方式，如下：

**第一种方式：**

在场景中添加一个 *Sprite* 作为圆球显示载体（把属性 `Texture` 设置为圆球图片），既然我们需要做自由落体，那么也就是需要一个刚体，所以我们给 *Sprite* 添加刚体属性，如果你学过 [Unity](https://link.zhihu.com/?target=https%3A//unity3d.com/) 的话，那么你会很熟练地在对应的 *GameObject* 上添加一个*Rigidbody2D Component* ，即所谓的刚体组件，然后设置刚体的质量、弹力、角速度等，在 Godot 中理论是一样的，但是实现却不一样，我们实现刚体特性是通过添加其他**功能子节点**来实现父节点的相关特性的。这里我们选中 *Sprite* 节点，按 *Ctrl+A* 快捷键添加一个 *RigidBody2D* 节点，接着出现一个警告小三角，点击它会有如下提示：



![img](https://pic4.zhimg.com/80/v2-e5ac05c246b35a59fb0aff6e7df47f53_720w.jpg)RigidBody2D warning





意思很清楚，就是告诉你， *RigidBody2D* 刚体节点没有碰撞形状节点是不能进行正常物理交互的！解决这个问题很简单，给 *RigidBody2D* 添加一个 *CollisionShape2D* 的子节点就 OK 了，这时候你会发现另一个警告：



![img](https://pic4.zhimg.com/80/v2-24f376623b6607f5571553b91a788e43_720w.jpg)CollisionShape2D warning





同样的道理， *CollisionShape2D* 也需要一个实实在在的形状来进行碰撞交互，这个形状的创建非常简单，选择 *CollisionShape2D* ，在它的属性面板里的 `Shape` 属性下点击选择 `New CircleShape2D` 创建一个圆形碰撞体，场景中立刻出现一个蓝色的圆，这个圆就是用于物理交互的碰撞体，碰撞体形状默认大小很小，我们可以点击 *Shape*里刚才创建的这个圆形碰撞体进入 *CircleShape2D* 的详细设置面板，然后设置半径`Radius` 为 28 就差不多和圆形 *Sprite* 大小相当了。



![img](https://pic2.zhimg.com/80/v2-c60a3d79cc324bd510c2b0a75e76dd51_720w.jpg)godot_2_collisionshape2d_shape





第一种方案算是完成了，运行游戏，结果出乎意料？圆球纹丝不动！什么原因呢？是不是没设置重力或者质量？哈哈，别急，卖个关子，看了第二种方案你就会理解了。 :sunglasses:

**第二种方式**

Godot 中的节点非常强大，而且又不失灵活性！既然 *RigidBody2D* 表示的就是刚体，而 *Sprite* 仅仅只是作为一个图片显示的载体，那我们是不是可以把 *Sprite* 作为*RigidBody2D* 的子节点而提供图片显示作用，而 *RigidBody2D* 作为父节点提供真实的物理交互功能呢？按此理论，我们开启第二种方式。

在第一种方式的基础上，我相信大家对添加节点的操作应该比较熟悉了，直接 *Ctrl+A* 添加相关的节点，这里要注意的是： *RigidBody2D* 节点和刚才我们第一种方法中的*Sprite* 节点都是场景 *Game* 根节点的直接子节点，平起平坐，添加的时候别弄错了。

添加设置完节点后，为了区分两种不同的方式，我分别移动了他们的位置，你也可以直接在属性面板里设置两个父节点 *Sprite* 和 *RigidBody2D* 的 `Transform/Position`位置的值，记住一定是**父节点**，别弄错了！结果如图：



![img](https://pic3.zhimg.com/80/v2-e2fa6029a405821fc523db87a797a956_720w.jpg)godot_2_nodes_setting





经过两种方案后，我想你应该已经知道第一种方案不可行的原因了吧！没错，正是由于*Sprite* 并不会因为有一个 *RigidBody2D* 子节点而改变图片渲染位置，虽然子节点的位置受重力的影响会移动，而在第二个方案里， *Sprite* 作为 *RigidBody2D* 的子节点，父节点位置发生变化， *Sprite* 子节点相应跟随运动。如何证明？这里我们可以使用 Godot 强大又舒爽的 **Debug** 功能一探究竟：选择菜单栏的 Debug 菜单，勾选*Visible Collision Shape* ，然后运行，效果一目了然！ :laughing:









![img](https://pic3.zhimg.com/80/v2-d38c05da4e751584f2352b47d29235f2_720w.jpg)godot_2_debug_collision_shape



![img](https://pic1.zhimg.com/v2-5bdc46eb738950f0f126920342d54214_b.jpg)

## 丰富场景

这个 Demo 虽小，但是到此为止的话，那就有点无趣了，由于是自由落体运动，球体会永无禁止地运动下去！如何让它们落地呢？很简单，给我们的小游戏添加一个带碰撞体的地面就 OK 啦！

这里要说明的是，地面（静态）和刚体都具有碰撞物理特性，但是他们关键点在于：地面的碰撞体是静态的！所以这里我们使用 *StaticBody2D* 作为父节点，然后添加一个*Sprite* 图片作为显示渲染载体，制作一个简单的平铺地层。并没有什么难度，唯一要提醒的是怎么让我们的地面实现水平平铺（ Repeat-X ）以及使用 *SegmentShape2D* 作为静态碰撞体的交互形状，关于设置直接看图介绍吧：



![img](https://pic4.zhimg.com/80/v2-15e9db08e9a218172e4916dcba3d3c7b_720w.jpg)godot_2_sprite_repeatx

完成后，最终的效果如下：



![img](https://pic2.zhimg.com/v2-c20d665ae82d532aa1b3d28f4f82df05_b.jpg)







完成后，最终的效果如下：



最后的最后，我在地面碰撞体背景中使用的是 *SegmentShape2D* 而非 LineShape2D ，原因可以引用官方文档的解释，并在此建议大家在单向直线碰撞体中优先使用*SegmentShape2D* 吧：

> [LineShape2D](https://link.zhihu.com/?target=http%3A//docs.godotengine.org/en/3.0/classes/class_lineshape2d.html): Line shape for 2D collisions. It works like a 2D plane and will not allow any body to go to the negative side. Not recommended for rigid bodies, and usually not recommended for static bodies either because it forces checks against it on every frame.[SegmentShape2D](https://link.zhihu.com/?target=http%3A//docs.godotengine.org/en/3.0/classes/class_segmentshape2d.html): Segment shape for 2D collisions. Consists of two points, a and b.

## 总结

本篇讲解到的知识点：

1. 几个基本的节点添加和使用
2. 刚体碰撞体设置
3. 静态碰撞体设置
4. 材质背景平铺设置
5. 可视化 Debug 功能

本篇没有使用任何代码，仅仅利用 Godot 丰富的节点系统就完成了这个小 Demo ，算是入门中的入门吧，在后续文章中我会详细说明使用 [GDScript](https://link.zhihu.com/?target=http%3A//docs.godotengine.org/en/3.0/getting_started/scripting/gdscript/gdscript_basics.html) 代码来加强和丰富我们的游戏功能。嗯，估计新手朋友们早就想跃跃欲试了吧，你完全可以尝试给节点添加代码，实现一些基本的功能，其实 *GDScript* 非常简单，如 Python 兄弟般，嘿嘿。 :sunglasses:

## 三、其他

嗯，这次就这些，我本意是希望阅读我的文章的朋友们（特别是初学者）能有不错的收获，我也会尽量做到吧，当然，第一次做这种系列的文章，难题和问题在所难免，还请大家多多包涵，多多提出意见和建议，非常感谢！附上 Demo 的 Github 地址：[https://github.com/spkingr/Godot-Demos](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos) 。

好吧，下次继续，还是那句话：**原创不易**啊，希望大家喜欢！ :smile:



# Godot3游戏引擎入门之三：移动我们的主角

[![刘庆文](https://pic3.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

19 人赞同了该文章

一、前言

**说明：我目前使用的** **[Godot 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)，所以会与 Godot 3 的版本有一些区别，界面影响不大，如果要使用我上传的** **[Github Demo 代码](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos)，记得去官网[下载 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)（或者等之后正版发布）然后就可以正常打开运行 Demo 了。**



[刘庆文：Godot3游戏引擎入门之二：第一个简单的游戏场景24 赞同 · 5 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/44323442)

> 主要内容： Godot 2D 小游戏入门之使用键盘控制移动阅读时间： 4-5 分钟永久链接：[http://liuqingwen.me/blog/2018/09/18/introduction-of-godot-3-part-3-move-character-with-inputs/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/09/18/introduction-of-godot-3-part-3-move-character-with-inputs/)系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 了解图片材质在 Godot 中的导入功能
2. 创建简单的场景，调整节点渲染次序，给节点添加脚本
3. 简单的 GDScript 脚本功能介绍和使用

## 创建场景

首先是创建我们的游戏主场景，相比[上一节](https://zhuanlan.zhihu.com/p/44323442)，这个场景会更加简单，首先场景尺寸我在项目设置中设成了 600x600 ，添加一个 Node2D 节点作为根节点，并改名为 Game ，然后添加两个子节点，一个是我们的主角 Sprite 节点，命名为 Knight ，再添加一个 Sprite 节点作为游戏中的地面，单击，命名为 Ground ，接着修改相应的图片材质属性。这里的操作有几点需要注意：

**1. 图片的导入**

如果你滚动鼠标滚轮，放大我们的视窗，你会发现我们的主角：骑士的图片放大后有点模糊，这里我希望能像有些像素游戏一样能够清晰地显示图片各个像素（ 2D 游戏中一般叫完美像素： Pixel Perfect ），那样即使图片很小，像素化后依然显得更加逼真，如何在 Godot 中实现呢？非常简单， Godot 已经为我们预制好了，选中图片，在属性面板上方导入设置中进行相应的设置即可，非常简单，记得设置好之后一定要点击 Reimport 重新导入:

![img](https://pic4.zhimg.com/80/v2-f3d7e9f6d13d4b90e45381302b12cabb_720w.jpg)godot_3_reimport_image

经过像素设置，我们的主角图像放大后像素更加清晰，是不是感觉更加 2D 了？熟悉 Unity 的同学知道，其 2D 场景是伪 3D 场景打造所以并没有 Pixel Perfect 功能。想深入了解 Godot 中更多关于图片压缩模式的知识，可以参考官方的压缩文档：[Importing Images - Compression](https://link.zhihu.com/?target=http%3A//docs.godotengine.org/en/3.0/getting_started/workflow/assets/importing_images.html%23compression)

**2. 重铺图片导入**

接着是地面的图片设置，还是使用[上一节](https://zhuanlan.zhihu.com/p/44323442)中的图片，之前我已经提到了如何设置普通图片材质的平铺属性，不过，之前的设置在重新打开后会丢失，如果保存平铺设置？我们需要在图片导入的时候进行相关的设置，保存并重新导入即可，相关设置如下图：

![img](https://pic3.zhimg.com/80/v2-f3f25f0d65b4a46b10dc0637a6b3937e_720w.jpg)godot_3_texture_region

大致的步骤就是：先选中图片，启用 Repeat 功能，最后点击 Reimport 重新导入图片材质，接着选中地面 Ground 节点，开启图片的 Region 区域设置，设置高度和图片原高度相等，为 256 ，宽度设置为你想要的宽度，比如我设置的是 800 （或者更高）。最后你会发现我们的地面图片在宽度方向上会沿着 X 轴方向自动平铺， OK ，完美解决！

**3. 节点渲染顺序**

有一个小问题是在我们添加了两个子节点后，移动位置，我们的场景显示是这样的：

![img](https://pic4.zhimg.com/80/v2-292b0c1a8566ca1ac8c085aed59d010f_720w.jpg)godot_3_render_order.

主角干嘛躲在草丛后面啊？别怂，出来干啊！哈哈，其实原因在上图我已经说明了，这是由于 Godot 中节点的渲染顺序引起的，越在上面的节点，渲染顺序越前，所以下面的节点会最后渲染，造成的结果就是：可能会覆盖之前渲染的上面的一些节点。解决方案很简单，移动一下地面和主角节点的次序就可以了。

## 添加脚本

简单的场景打造好了，接下来就是如何使用键盘输入控制骑士的位置移动了，学习 GDScript 脚本语言的最佳时机到来，本篇作为脚本开场白，仅仅做一个简单的介绍，然后编写代码实现一些简单的功能。

在了解 GDScript 脚本之前，我想比较一下 Godot 与 Unity 脚本的一些共同点，如果你有游戏开发经验，你会发现他们有很多相似点。首先，我们选中 Game 根节点，然后在右上角点击添加脚本，创建一个简单的脚本文件，写上一些方法（ # 号代表注释，和其他语言里的 // 一样）：

```text
# 节点激活后运行该方法
func _ready():
    print('ready!')

# 每帧运行此方法
func _process(delta):
    print('process with delta time: ', delta)

# 处理物理引擎的方法
func _physics_process(delta):
    print('physics process with delta time: ', delta)

# 处理设备输入的方法
func _input(event):
    print('input event: ', event)

# 处理设备输入的另一个方法
func _unhandled_input(event):
    print('unhandled input event: ', event)
```

上面的代码通过方法名字和我的注释说明应该能明白它的含义了，现在看下 Unity 中 C# 脚本组件的语法：

```text
void Awake()
{
    Debug.Log("Awake");
}
void Start()
{
    Debug.Log("Start");
}
void Update()
{
    Debug.Log("Update: " + Time.deltaTime);
}
void LateUpdate()
{
    Debug.Log("LateUpdate: " + Time.deltaTime);
}
void FixedUpdate()
{
    Debug.Log("FixedUpdate: " + Time.deltaTime);
}
```

惊人的相似，不是吗？所以说，开发游戏有时候只是软件不同，思路大体还是相同的，正所谓道不同、理相同！好的，装逼到此结束！开始拿起笔头编写脚本吧，这里我把基本完工的脚本贴出来，你可以从英文单词释义或者我的注释中得到每一行代码的功能是什么样的，具体如下：

```text
# 继承于Node2D
extends Node2D

# 常量，表示速度（像素）
const SPEED = 200
# 定义一些变量，不需要类型
var maxX = 600 # 角色运动右边界
var minX = 0 # 角色运动左边界
var knight # 骑士节点

# 节点进入场景开始时调用此方法，常用作初始化
func _ready():
    # 获取节点并赋值给变量knight
    knight = self.get_node("Knight")

# 每一帧运行此方法，delta表示每帧间隔
func _process(delta):
    # Input表示设备输入，这里D和右光标表示往右动
    if Input.is_key_pressed(KEY_D) or Input.is_key_pressed(KEY_RIGHT):
        moveKnightX(1, SPEED, delta)
    elif Input.is_key_pressed(KEY_A) or Input.is_key_pressed(KEY_LEFT):
        moveKnightX(-1, SPEED, delta)
    
# 自定义函数，direction表示方向，speed表示速度，delta是帧间隔
func moveKnightX(direction, speed, delta):
    if direction == 0:
        return
    # position属性为节点当前置，Vector2向量简单乘法
    knight.position += Vector2(SPEED, 0) * delta * direction
    # 越界检测
    if knight.position.x > maxX:
        knight.position = Vector2(maxX, knight.position.y)
    elif knight.position.x < minX:
        knight.position = Vector2(minX, knight.position.y)
```

OK ，大功告成，运行我们的游戏，效果是这样的：

![img](https://pic4.zhimg.com/v2-662feb91ea0d0e070fde1bc2513bb14b_b.jpg)

不过……有点问题啊：主角显然能置身于场景之外啊，而且往左移动的时候居然是迈克尔杰克逊附身——没有转身！别急，解决方法非常简单：

*第一个：场景边界问题，在* *`_ready()`* *方法中的最后加入代码：*

```text
# get_rect方法获取节点边框
maxX -= knight.get_rect().size.x / 2
minX += knight.get_rect().size.x / 2
```

*第二个：左移转身问题，只需在* *`moveKnightX(...)`* *方法的最后加入代码：*

```text
# 节点的scale属性为缩放矢量
# 缩放矢量x值为1就是往右，-1表示往左缩放
knight.scale = Vector2(direction, 1)
```

终于完工，尽管没有真正的角色跑步动作（后续文章会讲解如何使用 Godot 强大的动画工具创建角色动画），但是我们的移动功能算是完整了，看图，最终结果：

![img](https://pic3.zhimg.com/v2-8ef705a99c76d894543aad3d442f4c2e_b.jpg)

## 三、总结

本篇讲解到的知识点：

1. 图片材质的导入模式
2. 节点渲染顺序
3. 最基础的 GDScript 脚本入门
4. 使用脚本获取节点属性，侦听输入控制主角移动

**PS: 我使用的是 Godot 3.1 版本，源码已经上传到 Github ，如果需要在 Godot 3.0 版本上运行你可以自行创建节点，把图片和代码复制过去即可，建议使用最新 3.1 预览版，因为 3.1 即将发布！哦吼！**



# Godot3游戏引擎入门之四：给主角添加动画（上）

[![刘庆文](https://pic1.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

12 人赞同了该文章

## 一、前言

**说明：我目前使用的** **[Godot 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)，所以会与 Godot 3 的版本有一些区别，界面影响不大，如果要使用我上传的** **[Github Demo 代码](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos)，记得去官网[下载 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)（或者等之后正版发布）然后就可以正常打开运行 Demo 了。**

本篇文章我会详细讲述 Godot 3 中制作动画的三种方式，篇幅有点长，所以分成上下两部分，请留意。 :smile:



[刘庆文：Godot3游戏引擎入门之三：移动我们的主角19 赞同 · 8 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/44897448)

> 主要内容： Godot 2D 小游戏入门之三种动画创建方式（前两种）
> 阅读时间： 10-15 分钟
> 永久链接：[http://liuqingwen.me/blog/2018/09/25/introduction-of-godot-3-part-4-add-some-cute-animations-part-1/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/09/25/introduction-of-godot-3-part-4-add-some-cute-animations-part-1/)
> 系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 使用动画精灵 AnimatedSprite 节点创建 Sprite 骑士动画
2. 使用 Sprite 节点和 GDScript 脚本代码共同创建背景滚动效果
3. 使用 AnimationPlayer 节点制作天鹅飞舞的关键帧动画

## 游戏场景

还是[上篇一样](https://zhuanlan.zhihu.com/p/44897448)的场景：绿油油的草地上站着一位能左右打滑的扛着大刀的小正太！嗯，不合格的武士只能打滑，不能跑，还不能正常呼吸，怎么看都不舒服，所以，我们这篇文章的任务就是：让他真正地动起来——给我们的游戏场景添加一些生动的动画元素。 :sunglasses:

由于涉及到动画，这会导致在 2D 游戏中图片资源数量急剧增加，不过别担心，我已经分门别类地放置好了，在 Godot 项目中可以使用文件夹管理资源，如下：

![img](https://pic2.zhimg.com/80/v2-381cccc367921546447511dc43df9da9_720w.jpg)godot_4_assets_folder.jpg

项目 Demo 已经上传到 Github ，您可以到我的 Github 主页上下载整个游戏的相关资源和代码，如果需要直接运行，请注意使用 [Godot 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)打开。

接下来，我们在原来场景的基础上：让我们的主角真正地跑起来，再增加一个卡通云朵飘过的天空，以及一只在天空中飞舞的勤奋的小天鹅。

## 创建动画

我们要添加的三个动画元素，分别使用三种方法制作，当然，你完全可以只选择其中一种或两种动画方式来完成，这取决于你，这里我只是把这几种常用方式都介绍一下，希望达到一个抛砖引玉的效果，哈哈。

**第一种方法：使用 AnimatedSprite 制作骑士动画**

这种方法使用非常简单但又不失强大，最适合于打造单个人物、物体的精灵动画特效。*AnimatedSprite* 制作动画的原理很简单：如同电影胶卷一样，一张一张图片播放，当播放速度达到一定程度，就感觉是在播放动画了！

![img](https://pic2.zhimg.com/80/v2-b700dce89929a68343af3bfd88674561_720w.jpg)godot_animation_frame.jpg

如果你有使用过 Apple iOS 的 [SpriteKit](https://link.zhihu.com/?target=https%3A//developer.apple.com/spritekit/) 框架的经验，那么你会发现这种动画制作方式在游戏开发中使用是非常频繁的。 Godot 中使用的是 *AnimatedSprite* 节点，制作动画非常简单，你需要准备的是**很多张**主角的一系列动作图片即可。本次 Demo 中我们将应用到骑士两种动作状态： *idle* 休息状态和 *run* 奔跑状态。

<iframe title="video" src="https://video.zhihu.com/video/1028313066970210304?player=%7B%22autoplay%22%3Afalse%2C%22shouldShowPageFullScreenButton%22%3Atrue%7D" allowfullscreen="" frameborder="0" class="css-uwwqev" style="width: 688px; height: 387px;"></iframe>

逐帧动画-迪士尼片头

理论说多了，不如实践！我们开始动工。首先，和[上一篇](https://zhuanlan.zhihu.com/p/44897448)不一样，我们不使用 *Sprite* 创建主角，取而代之的是 *AnimatedSprite* 动画精灵节点，添加节点后改名为 *Player* ，操作结果如下图，忽略节点后的警告小三角形：

![img](https://pic4.zhimg.com/80/v2-4a43014ee7a2d3e214ae14b057523c63_720w.jpg)godot_4_scene_and_animatedsprite.jpg

接下来按上图，先选中 *Player* 骑士玩家（ *AnimatedSprite* 节点），在属性面板*Frames* 下点击新建一个 *SpriteFrames* 即所谓的*精灵帧组*，创建完后点击 *Open Editor* 打开精灵帧动画编辑工具面板（**注意：此处和 Godot 3.0 版本略有区别，之前的版本中无此按钮，也不需要点击此按钮！**），主界面下方就出现了我们创建主角各种动画状态的工作区域了。这里我们创建两个动画，分别命名为 *idle* 和 *run* ，然后对应地把各自状态的 10 张图片（命名 (1) 到 (10) ）拖到空白内容栏即可，步骤如下：

![img](https://pic3.zhimg.com/80/v2-2951e9b3a747cafef503b5ec0ac08cd2_720w.jpg)godot_4_spriteframes_editor.jpg

完成后，我们需要调整每个状态动画的帧率（ *FPS* ），也就是每秒显示几帧或者几张图片。我这里设置 *idle* 状态是 8 FPS ，跑步 *run* 动画状态是 16 帧每秒，你可以按需设置，接着选中骑士玩家节点，在属性面板，如上面第二张图中突出部分，勾选 Playing 选项框，然后在 *Animation* 属性中选择你想查看的动画状态（ *idle/run* ）就可以在编辑器中实时查看人物动画效果了，是不是很贴心啊？

![img](https://pic3.zhimg.com/80/v2-b5bb88a36abee4fb273ff21cd34950aa_720w.jpg)godot_4_animatedsprite.jpg

不知道你的感觉是怎样，反正我感觉 Godot 的动画精灵非常简单又灵活，其实在 Unity 中也有帧动画，即 *Animation* ，但是在 Unity 中创建动画相对 Godot 要繁琐点，需要创建帧，然后一帧一帧地设置图片，最后需要创建 *Animator Controller* ，在 Godot 中可以直接拖拽一步到位，设置也非常简单。

第一种方式基本完成，接下来就是控制显示玩家的状态了，原理非常简单：如果玩家移动，那么把玩家节点的动画状态调整为 *run* ，否则设置为 *idle* 静止。参考上一篇的代码， 新增核心代码如下：

```text
# ...省略一些代码，和上一篇文章代码一样
# ...可以在 Github 上下载源代码
func _process(delta):
    # Input表示设备输入，这里D和右光标表示往右动
    if Input.is_key_pressed(KEY_D) or Input.is_key_pressed(KEY_RIGHT):
        moveKnightX(1, SPEED, delta)
        return # 有设备输入，直接返回
    elif Input.is_key_pressed(KEY_A) or Input.is_key_pressed(KEY_LEFT):
        moveKnightX(-1, SPEED, delta)
        return # 有设备输入，直接返回
    
    # 没有键盘控制，让骑士动画设置为idle状态
    if knight.animation != 'idle':
        knight.animation = 'idle'

# 自定义函数，direciton表示方向，speed表示速度，delta是帧间隔
func moveKnightX(direction, speed, delta):
    # 控制骑士移动，让骑士动画为run状态，跑起来
    if knight.animation != 'run':
        knight.animation = 'run'
    
    # ...省略其他代码，和上一篇文章代码一样
```

运行以下，效果如图：

![img](https://pic3.zhimg.com/v2-76da73974d9b16327b6c2e011e7920de_b.jpg)

**第二种方法：使用代码控制背景天空滚动**

现在进入第二种动画方式，相对第一种，这种方式可以说是最符合*程序员*直觉的：直接控制移动背景图片的位置就能达到我们想要的效果。所以，为了让云朵动起来，我们需要一点点代码。在编写代码之前，我们先搞懂一个 2D 游戏中经常遇到的概念：原点（*Origin* ）位置。

在 Godot 中坐标系原点位于舞台的左上角，往右为 x 正方向，往下为 y 正方向，和大部分手机游戏框架类似，同时 *Sprite* 图片精灵的原点位置默认为图片的正中心点，所以当图片坐标为坐标系原点 (0, 0) 的时候，图片只有右下角部分显示在场景中，想要图片从左上角开始全部位于场景中，需要往右下方向移动图片大小的一半，这样我们使用代码处理起来很不方便，如果能把图片的原点位置置于图片左上角（比如 Adobe Flash 中的*Sprite/MovieClip* 默认如此），那处理起来会更加方便，可否这样设置呢？——当然可以！

首先，我创建了两个一模一样的 *Sprite* 节点，分别命名为 *Sky1* 和 *Sky2* ，材质属性也一模一样，都是一张天空背景图，选中每一个节点，在节点属性的 *Offset* 下，取消勾选 *Center* ，即取消居中即可，比较一下两种方式的显示异同：

![img](https://pic2.zhimg.com/80/v2-0ace43fdf689d29cec29ae1987520811_720w.jpg)godot_4_origin_center.jpg

设置好之后，接下来就是编写代码了，代码的工作原理大致是这样的： *Sky1* 和 *Sky2*挨着放置在一起，同时往左移动，当左边那张图移出舞台的左边界后，马上移动到右边那张图后面，倒换顺序，继续滚动，如此循环以实现背景的无视差连续运动：

![img](https://pic2.zhimg.com/v2-03c14c8ad0b86d1575e24c29430d836d_b.jpg)

最终实现效果如上图，主要代码如下，这里我介绍了两个关键词： `onready` 和 `$`，用法我在注释中有说明：

```text
# ...省略一些代码，和上一篇文章代码一样

# onready关键词使变量在场景加载完后赋值，保证不为null
# 效果和上一篇在 _ready() 方法中初始化一样
onready var knight = self.get_node("Knight")
# 在Godot中$符号可以直接加子节点名字获得子节点对象
# $Sky1相当于self.get_node("Sky1")
onready var sky1 = $Sky1
onready var sky2 = $Sky2

func _process(delta):
    # 移动背景天空位置，生成滚动动画
    updateSkyAnimation(SKY_SPEED * delta)
    # ...省略一些代码

# 移动背景天空位置，生成滚动动画
func updateSkyAnimation(speed):
    # 移动，更新背景的位置
    sky1.position.x -= speed
    sky2.position.x -= speed
    # 如果滚动到最左边，那么移动到右边来
    if sky1.position.x <= -1200:
        sky1.position.x += 2400
    elif sky2.position.x <= -1200:
        sky2.position.x += 2400
```

**第三种方法：使用 AnimationPlayer 关键帧制作天鹅动画**

第三种方法将下一篇： [Godot3 游戏引擎入门之四：给主角添加动画（下）](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)中介绍。

## 三、小结（上）

好了，上部分的两种动画方式都已经介绍完毕，剩下第三种动画制作方法介绍先卖个关子吧，一次性阅读文章太长不好掌握，而且还附有不少源代码，所以留给下篇。

总结一下本篇讲解到的 Godot 3 中的知识点：

1. 使用 AnimatedSprite 节点创建多个多图动画
2. 使用 Sprite 节点和 GDScript 脚本代码创建背景动画
3. 介绍了 Sprite 节点的原点设置：左上角或者居中
4. 相关 GDScript 脚本知识：`onready/$/position/animation`



# Godot3游戏引擎入门之四：给主角添加动画（下）

[![刘庆文](https://pic1.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

11 人赞同了该文章

## 一、前言

本篇是上一节文章：[Godot3游戏引擎入门之四：给主角添加动画（上）](https://zhuanlan.zhihu.com/p/45399217)的继续。在这两篇文章里，我会详细讲述 Godot 3 中制作简单精灵动画的三种方法，其中上部分包含两种，下部分讨论第三种方式。 :smile:



[刘庆文：Godot3游戏引擎入门之四：给主角添加动画（上）12 赞同 · 5 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/45399217)



> 主要内容： Godot 2D 小游戏入门之三种动画创建方式（第三种）
> 阅读时间： 8-10 分钟
> 永久链接：[http://liuqingwen.me/blog/2018/09/27/introduction-of-godot-3-part-4-add-some-cute-animations-part-2/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/09/27/introduction-of-godot-3-part-4-add-some-cute-animations-part-2/)
> 系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 使用动画精灵 *AnimatedSprite* 节点创建 *Sprite* 骑士动画（上篇）
2. 使用 *Sprite* 节点和 *GDScript* 脚本代码共同创建背景滚动效果（上篇）
3. 使用 *AnimationPlayer* 节点制作天鹅飞舞的关键帧动画（下篇）

## 创建动画

首先，简单回顾一下本篇上节内容中的两种游戏动画制作方式：

**第一种方法：使用 AnimatedSprite 制作骑士动画**

非常简单又符合直觉的一种方法，最适合于打造单个人物或物件的精灵动画特效。*AnimatedSprite* 制作动画的原理相当简单，只需要提前准备好必须的图片资源即可，具体操作参考上节的内容。

![img](https://pic3.zhimg.com/v2-76da73974d9b16327b6c2e011e7920de_b.jpg)

**第二种方法：使用代码控制背景天空滚动**

这种方式相对第一种可以说是最符合*程序员*的思维习惯的的：通过代码直接控制并移动背景图片的位置就能达到我们所想要的动画特效。在上一节内容中，我们还了解到了 Godot 中图片的坐标原点位置的相关设置。

![img](https://pic2.zhimg.com/v2-03c14c8ad0b86d1575e24c29430d836d_b.jpg)

**第三种方法：使用 AnimationPlayer 关键帧制作天鹅动画**

上文介绍的两种动画制作方式简单也不失灵活性，在实际游戏开发过程中使用的也会比较多，但是，如果你认为 Godot 就这点能耐的话，那你也太小看它了，哈哈。接下来我们开始探讨第三种动画制作方式：关键帧动画！现在，隆重请出我们今天的主角：*AnimationPlayer* ！ :sunglasses:

![img](https://pic1.zhimg.com/80/v2-beadec43eb5603de52e0395471d1eddc_720w.jpg)godot_animation_keyframe.jpg

在深入讨论之前，我们先了解一下 *SpriteSheet* 相关知识，如果你有使用过 [LibGDX](https://link.zhihu.com/?target=https%3A//libgdx.badlogicgames.com/)跨平台游戏框架开发游戏的经验，或者熟悉 Unity 中的 2D 游戏动画制作，那么你肯定对 *SpriteSheet* 会非常了解。我们想象一下第一种动画方式，使用 *AnimatedSprite*制作动画虽然简单，但是如果涉及到人物多种状态，比如攻击、跳跃、行走、死亡等，那么图片资源是不是会多如牛毛？而且操作过程中还容易出错，这就是 *SpriteSheet* 的由来之处了！简而言之， *SpriteSheet* 就是把很多图片，甚至不同类型的图片资源，放到一个大图片里，方便管理操作和使用，听说过 [TexturePacker](https://link.zhihu.com/?target=https%3A//www.codeandweb.com/texturepacker) 这个软件吗？它就是专门干这事的。

理论到此结束，我们来瞻仰一下我们要实现的天鹅动画的图片资源 *SpriteSheet* 精灵图集：

![img](https://pic3.zhimg.com/80/v2-d262e24c15439d3fea90652838830a32_720w.jpg)godot_4_swansheet.png

图片结构很单一，可以看得出是由 8 张连续的小图拼接而成的，怎么使用呢？首先，我们还是和往常一样使用一个 *Sprite* 精灵节点来显示天鹅图片，改名为 *Swan* ，但是这里还需要进行一些简单的设置：

![img](https://pic3.zhimg.com/80/v2-dcd12c550c286facd306760d35ad374e_720w.jpg)godot_4_hframes.jpg

如上图，我们设置属性 *Vframes* 值为 1 ， *Hframes* 为 8 ，意思很明确，即纵向分 1 帧，横向分 8 帧，然后总共 1x8 帧，而第三个属性 *Frame* 就表示当前显示第几帧画面，可以设置为 0-7 共 8 帧画面，操作浏览一下效果试试，你会发现 *Frame* 值从 0 到 1 然后慢慢设置到 7 的时候，天鹅图片就产生了一种不连续的动画效果，对，动画原理就是这么简单！这个时候你会想：我如果在代码中获取 *Swan* 的 *Frame* 属性，然后把它的值每次往前加 1 不就可以生成动画了吗？的确可以！代码如下：

```text
func _process(delta):
    if $Swan.frame == 7:
        $Swan.frame = 0
    else:
        $Swan.frame += 1
```

这和第二种方法的道理完全相同，也很值得一试！不过运行游戏场景后，你会发现天鹅飞舞的动画太快了！当然，这并不是什么大问题，添加一个时间控制的变量，让帧属性慢点往前加 1 就可以了。不过这不是我们要讨论的重点，我所要给大家介绍的是 Godot 中强大到能够控制一切的关键帧动画节点工具： *AnimationPlayer* ！

对，在 Godot 中 *AnimationPlayer* 的确能操纵一切，简单的如位置、旋转、缩放的控制，还有其他节点的任意属性值的控制，甚至连方法的调用都能在 *AnimationPlayer* 中进行动画设定！同时，不仅强大，使用起来也非常简单。如何实现天鹅动画，这里我做了一个简单的操作示意图，大家可以感受下 *AnimationPlayer* 节点的使用步骤：



godot_4_keyframes.gif

下面进入细节部分，首选我们需要在游戏根节点下创建一个 *AnimationPlayer* 节点，这里要强调一下：我们要对 *Swan* 节点进行动画，所以他们需要放置在同一级别上！当然，*AnimationPlayer* 完全可以同时对其他节点比如*天空背景*或者*主角骑士*节点进行动画，你可以尝试一下。接下来，选择 *AnimationPlayer* 节点，新建一个动画轨道：

![img](https://pic4.zhimg.com/80/v2-0934a5bcd7a776f29346d1245337d8eb_720w.jpg)godot_4_create_animation.jpg

然后对我们新建的动画轨道进行设置：自动播放、重复播放、动画时长等，部分细节如下图：

![img](https://pic4.zhimg.com/80/v2-766853d84a197c34088dfaa92100922f_720w.jpg)godot_4_keyframes_setting.jpg

OK ，大功告成，运行结果：

![img](https://pic2.zhimg.com/v2-b284a877c3cdfd751f42bf76a676c801_b.jpg)

最后，虽然动画有了但是天鹅并不能移动位置，我们需要让它随着时间不断移动位置就可以了。这里介绍一个小技巧：我们可以直接在节点上添加脚本！ Godot 推荐我们这么做，尽量让每一个节点独立，也就是和整个游戏场景**解耦**，在大项目中让合作开发更高效。

Talk is cheap, show me the code! **选择 Swan 节点**，点击添加脚本，编写代码：

```text
extends Sprite

# 速度常量
const SPEED = 100
# 最左边界和最右边界
var minX = -100
var maxX = 800

func _process(delta):
    position.x -= SPEED * delta
    # 如果天鹅飞到左边边界，把它的x坐标置为最右边界
    if position.x < minX:
        position.x = maxX
```

最终效果：

![img](https://pic4.zhimg.com/v2-4f5109915796b4ad76d4d10d233bdbfb_b.jpg)

## 所有代码

我们的游戏终于完成了，这里我附上所有的代码，如果你已经阅读过前面两篇文章：[Godot3游戏引擎入门之三：移动我们的主角](https://zhuanlan.zhihu.com/p/44897448)，那么请跳过。

```text
# 继承于Node2D
extends Node2D

# 常量，表示速度（像素）
const SPEED = 200
const SKY_SPEED = 50
# 定义一些变量，不需要类型
var maxX = 600 # 角色运动右边界
var minX = 0 # 角色运动左边界
# onready关键词使变量在场景加载完后赋值，保证不为null
onready var knight = self.get_node("Knight")
# 在Godot中$符号可以直接加子节点名字获得子节点对象，相当于get_node方法
onready var sky1 = $Sky1
onready var sky2 = $Sky2

# 节点进入场景开始时调用此方法，常用作初始化
func _ready():
    maxX -= knight.frames.get_frame('idle', 0).get_size().x / 2
    minX += knight.frames.get_frame('idle', 0).get_size().x / 2

# 每一帧运行此方法，delta表示每帧间隔
func _process(delta):
    # 移动背景天空位置，生成滚动动画
    updateSkyAnimation(SKY_SPEED * delta)
    
    # Input表示设备输入，这里D和右光标表示往右动
    if Input.is_key_pressed(KEY_D) or Input.is_key_pressed(KEY_RIGHT):
        moveKnightX(1, SPEED, delta)
        return
    elif Input.is_key_pressed(KEY_A) or Input.is_key_pressed(KEY_LEFT):
        moveKnightX(-1, SPEED, delta)
        return
    # 没有键盘控制，让骑士动画为idle状态
    if knight.animation != 'idle':
        knight.animation = 'idle'

func updateSkyAnimation(speed):
    # 移动，更新背景的位置
    sky1.position.x -= speed
    sky2.position.x -= speed
    # 如果滚动到最左边，那么移动到右边来
    if sky1.position.x <= -1200:
        sky1.position.x += 2400
    elif sky2.position.x <= -1200:
        sky2.position.x += 2400
    
# 自定义函数，direciton表示方向，speed表示速度，delta是帧间隔
func moveKnightX(direction, speed, delta):
    # 有键盘控制，让骑士动画为run状态，跑起来
    if knight.animation != 'run':
        knight.animation = 'run'
    
    if direction == 0:
        return
    # position属性为节点当前置，Vector2向量简单乘法
    knight.position += Vector2(speed, 0) * delta * direction
    # 越界检测
    if knight.position.x > maxX:
        knight.position = Vector2(maxX, knight.position.y)
    elif knight.position.x < minX:
        knight.position = Vector2(minX, knight.position.y)
    
    knight.scale = Vector2(direction, 1)
```

## 三、小结（下）

三种方式已经全部讲解完毕，这里简单总结一下 Godot 3 中动画制作三种方式的优缺点：

- **AnimatedSprite**

优点 | 简单明了，最适合制作主角多种状态动画

缺点 | 只能使用图片，而且必须使用很多张图片，资源文件数量大增

- **Sprite + GDScript**

优点 | 思路清晰，适合简单的动画，代码可控度高

缺点 | 对于复杂的属性动画很难使用代码达到理想效果

- **AnimationPlayer**

AnimationPlaye


优点 | 最强大的动画系统，几乎能操纵一切元素来实现复杂的动画

缺点 | 仅仅操作稍复杂点，节点的位置必须同级别



# Godot3游戏引擎入门之五：上下左右移动动画（上）

[![刘庆文](https://pic1.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

9 人赞同了该文章

## 一、前言

前面的几篇文章陆陆续续开始介绍 2D 游戏中对玩家的一些基本操作流程了，不过功能实现非常有限，接下来我想完完整整的打造一个小 Demo ：在封闭的游戏场景里控制玩家自由移动，从而达到一些简单的目标。那么， first thing first ，从解决*上下左右*移动功能实现开始！

上下左右移动也叫 *Top-down* 移动动画，这篇文章我会通过 Godot 中的节点以及相关的代码来实现玩家主角的基本移动控制。之后，再改造一下游戏场景，让我们的主角自由行走在有限的世界里。一如往常，老司机带路，如果你是编程新手，那么，前方高能请系好安全带啦！当然，前面的文章也讨论过了， GDScript 脚步非常简单，不熟悉的话可以浏览一下本系列之前的文章。

> 主要内容： Godot 2D 中玩家的上下左右移动及碰撞实现
> 阅读时间： 5 分钟
> 永久链接：[http://liuqingwen.me/blog/2018/10/10/introduction-of-godot-3-part-5-the-basic-top-down-movement-part-1/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/10/10/introduction-of-godot-3-part-5-the-basic-top-down-movement-part-1/)
> 系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 使用 AnimationPlayer 节点工具创建状态动画
2. 使用代码控制玩家的上下左右移动功能
3. 简单的摄像机使用和地图碰撞检测实现
4. 通过代码实现 RigidBody2D 刚体节点的运动

## 创建动画

相信看了[上篇文章](https://zhuanlan.zhihu.com/p/45595965)的朋友应该对 *AnimationPlayer* 这个功能强大的动画工具有了一定的了解。之前只是利用它最基础的功能实现了一个简单的天鹅飞舞动画，接来下我们要使用*AnimationPlayer* 节点实现稍微复杂的动画制作——玩家的各种状态动画实现。

我们先创建一个场景，根节点改名为 *Game* ，添加两个子节点： *Sprite* （命名为*Player* ）和 *AnimationPlayer* 节点。 *Player* 节点的图片材质是一张 4x5 的 SpriteSheet 精灵图集，四行分别代表下、左、右、上移动动画：

![img](https://pic2.zhimg.com/80/v2-dfba85e1e7c9a229d1de733b213c9e59_720w.jpg)player_sprite_sheet

和上篇文章制作天鹅动画操作一样，分别制作四个移动动画，这四个动画都设置为循环播放，动画时长和步进大家可以自己尝试进行设置不同的时间，直到自己满意为止吧，我的就随便设置了： 时长 0.8 ，步进 0.2 ，具体设置参考上一篇文章：

[刘庆文：Godot3游戏引擎入门之四：给主角添加动画（下）11 赞同 · 5 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/45595965)

。接下来才是重点：我们制作一个游戏启动时刻玩家入场动画。其实这个游戏大可不必这样做，完全是为了演示 *AnimationPlayer* 的强大功能，并增加一些喜感吧，当然也有一定借鉴意义，哈哈。

玩家 *Player* 入场动画的基本思路是这样的：主角从场景中央稍微偏上的位置快速移动到屏幕中央（ `position` ），同时尺寸由小逐渐放大到正常缩放（ `scale` ），并伴随透明度从*完全透明*到*完全不透明*（ `modulate/a` ），动画最后再加上一段玩家闪现的动画进行强调（ `visible` ）。哈哈，颇有主角粉墨登场的戏份啊！欢呼吧，骚年~ :sunglasses:

思路有了，关键在于使用 *AnimationPlayer* 来进行创建了。之前的动画制作都是一个轨道解决一个动画，但是这个动画不同了，需要一个动画实现多个属性的控制，这里就需要多个轨道了，每个属性分别创建一个轨道，然后对属性设置关键帧进行动画控制，这里需要注意的第一点是： Godot 3.1 alpha 版本中对**位置和缩放**属性不能直接使用**钥匙 ️**按钮创建相应的轨道和关键帧，会重复创建轨道，这应该是一个 Bug ，不过不要紧，我们使用普通的做法，手动创建 `Property Track` 属性轨道，选择 *Player* 节点的相应属性，之后可以正常使用**钥匙 ️**按钮创建关键帧，部分操作如下图：

![img](https://pic3.zhimg.com/80/v2-92bb425948b76076f266b732075b7f4a_720w.jpg)godot_5_property_track

上图中的*勾选贝塞尔曲线过渡方式*大家可以尝试一下，看看和平滑过渡有什么不同的效果吧。接下来，动画中透明度的设置是通过 *Sprite* 节点的 *Modulate* 颜色属性的*Alpha(A)* 通道设置实现的，至于闪现是通过控制节点的可见性 *Visible* 属性实现的，只要是属性， *AnimationPlayer* 就能创建动画，就是这么强！

![img](https://pic4.zhimg.com/80/v2-58c9340fc0ea7f517f8e7e113d89348f_720w.jpg)godot_5_visible_and_color

最后记得把入场动画（名为 `start` ）设置为**自动播放**，不要设置循环播放，毕竟主角登场了就不要重复了。

## 代码控制

动画制作完后的任务就交给代码来实现了！代码和上一篇文章里的左右移动代码没啥本质区别，只是多了两个方向而已，不过有两点新鲜玩意。第一个是我设置了速度变量，它是一个 `Vector2` 矢量，这样做的目的是：即使我们同时按住两个按键，玩家依然可以跑动或者原地踏步！大家可以体会下和上一节的不同之处。

第二个可谓是一个可以“节约生命”的功能，还记得上一节里怎么监控按键的吗？需要一个一个的常亮比如： `KEY_A/KEY_LEFT` 表示 *A* 键和左方向键。如果你是 Unity 的开发者，那么你对按键设置肯定非常熟悉，这里我不得不说 Unity 在这方面做得还是非常棒的，对键盘、操纵杆的控制设置很到位。 Godot 中同样也可以进行简化设置，比如把*A* 键和左方向键统一到自定义按键 `left` 中，具体设置在 *Project Settings* 中的*Input Map* 下添加自定义输入控制：

![img](https://pic3.zhimg.com/80/v2-1495b1bc15a91d36a889720c4db65e76_720w.jpg)godot_5_keyboard_settings

设置完就可以开森地写代码了：

```text
extends Node2D

onready var player = $Player
onready var animationPlayer = $Player

var currentAnimation = 'start'
var speed = 200

func _ready():
    camera.position = player.position

func _process(delta):
    var velocity = Vector2(0, 0) # 速度变量
    var isMoving = false # 是否按键移动
    var newAnimation = currentAnimation # 动画变量

    if Input.is_action_pressed('left'):
        velocity.x += -1
        newAnimation = 'left'
        isMoving = true
    if Input.is_action_pressed('right'):
        velocity.x += 1
        newAnimation = 'right'
        isMoving = true
    if Input.is_action_pressed('up'):
        velocity.y += -1
        newAnimation = 'up'
        isMoving = true
    if Input.is_action_pressed('down'):
        velocity.y += 1
        newAnimation = 'down'
        isMoving = true

    # 速度不为0，移动玩家位置
    if velocity.length() > 0:
        # 注意这里 normalize 速度矢量，否则会出现斜着走速度比单方向速度快
        player.position += velocity.normalized() * speed * delta

    # 根据是否有按键按下和新动作更新动画
    updateAnimation(isMoving, newAnimation)

func updateAnimation(isMoving, newAnimation):
    # 如果有移动按键按下，并且改变方向，则切换动画
    if isMoving and currentAnimation != newAnimation:
        animationPlayer.current_animation = newAnimation
        animationPlayer.play(newAnimation)
        currentAnimation = newAnimation
    # 未移动，但又非开始的情况，那么止移动动画
    elif ! isMoving and currentAnimation != 'start':
            animationPlayer.stop()
            currentAnimation = 'start'
    # 其他情况比如同方向继续移动，或者在开始的时候都不用处理
```

完成后效果：

![img](https://pic3.zhimg.com/v2-f01d3c6e281fb772c0505a70406883aa_b.jpg)

## 摄像机节点

对于上面实现的效果感想如何？嗯，移动是没问题了，入场动画有，只是没有录制进来，有兴趣的朋友可以到 [Github](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos) 上下载源码自己运行看看效果。不过，问题是，玩家完全可以脱离视野离家出走啊——所谓破墙而走！三种解决方式：

1. 第一种是限制移动，让玩家在固定视窗内行动，即通过判断玩家位置坐标计算有没有超出限制范围，上一篇介绍过了
2. 第二种是使用物理碰撞，把假的墙壁设置为真实的墙壁，这种方式下面会将
3. 第三种是非正面解决方式，即给我们的游戏添加一个摄像机，而这个摄像机时刻跟随主角运动，那么主角就不会脱离视野了

好吧，后面两种是这篇文章的目标，对于设置摄像机，和其他游戏引擎没有区别：添加一个摄像机节点，设置一下就好了，非常简单。在 Godot 中摄像机节点是 *Camera2D* ，添加一个节点到游戏场景后，我们通过代码控制摄像机保持和玩家位置一致，这里唯一一个要设置的地方就是：勾选 *Camera2D* 的 *Current* 属性，激活摄像机。同时，我还稍微拉伸了镜头，使得游戏场景被放大——通过设置摄像机的 *Zoom* 参数实现。

![img](https://pic2.zhimg.com/80/v2-8f352747eed6909094b9b071a4cd695d_720w.jpg)godot_5_camera_viewport

上图中，最下方的文字说明了视窗属性的设置：视口模式 *Mode* 为 *2d* ，缩放模式*Aspect* 设置为 *keep* ，即保持比例，这些设置都在 *Project Settings* 里能找到。作用很简单，如果不设置，那么默认情况下，我们的游戏进入全屏状态后是不会进行缩放的，就像下面这样：

![img](https://pic3.zhimg.com/80/v2-4400b9dfb6a818028f510453e009b48a_720w.jpg)

最后在 `player.position += velocity.normalized() * speed * delta` 这一句后面添加一点代码：

```text
# 省略代码......

# 速度不为0，移动玩家位置
if velocity.length() > 0:
    # 注意这里 normalize 速度矢量，否则会出现斜着走速度比单方向速度快
    player.position += velocity.normalized() * speed * delta
    # 更新摄像机，玩家始终在视窗内活动
    updateCameraPosition()
    # 省略代码......

func updateCameraPosition():
    camera.position = player.position
```

运行游戏，查看效果：

![img](https://pic3.zhimg.com/v2-c020025c43ec29ceaad31f31916d81c2_b.jpg)

接下来解决玩家移动无范围限制的问题。 :smiley:

## 添加碰撞

文章有点长，偷下懒，暂时到这里，接下来的内容放到下一节。 Stay tuned!

## 三、小结（上）

除了代码，这是一篇非常简单的文章，使用 *AnimationPlayer* 制作多个动画，以及单个动画多个轨道；使用 *Camera2D* 跟随玩家移动视野；设置按键规则和视窗缩放属性等。接下来的重点就交给本章的下节吧。

假期没有更新，带孩子在外面和家里玩了 8 天，哈哈！话说回来，嗯，还是那句：**原创不易**啊，希望大家喜欢！ :smile:

# Godot3游戏引擎入门之五：上下左右移动动画（下）

[![刘庆文](https://pica.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

9 人赞同了该文章

## 一、前言

本篇是上一节文章：

[刘庆文：Godot3游戏引擎入门之五：上下左右移动动画（上）9 赞同 · 6 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/46611931)

的继续。上一篇使用动画和代码实现了玩家的上下左右移动功能，接下来我们解决一个问题：给游戏添加碰撞体，让玩家在有限的地图中移动。

**注意：我目前使用的是** **[Godot 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)，与 Godot 3.0 正式版有一些区别，不过界面上影响不大，如果要使用我所上传的** **[Github Demo 代码](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos)，记得去官网[下载 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)然后就可以正常打开运行 Demo 了。 Good luck!**

> 主要内容： Godot 2D 中玩家的上下左右移动及碰撞实现
> 阅读时间： 4-5 分钟
> 永久链接：[http://liuqingwen.me/blog/2018/10/11/introduction-of-godot-3-part-5-the-basic-top-down-movement-part-2/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/10/11/introduction-of-godot-3-part-5-the-basic-top-down-movement-part-2/)
> 系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 使用 AnimationPlayer 节点工具创建状态动画（上）
2. 使用代码控制玩家的上下左右移动功能（上）
3. 简单的摄像机使用和地图碰撞检测实现（上下）
4. 通过代码实现 RigidBody2D 刚体节点的运动（下）

## 场景和代码

基本场景的制作已经在上篇中详细解说过了，另外我们还在场景中增加了一个 *Camera2D*摄像机节点，让场景的视窗时刻聚焦在玩家周围，但是玩家依然可以“鲤鱼跃龙门”，对场景中的墙壁视而不见，豪迈奔放！游戏运行结果如下：

![img](https://pic3.zhimg.com/v2-c020025c43ec29ceaad31f31916d81c2_b.jpg)

接下来利用物理引擎相关知识解决玩家移动范围限制的问题。

## 添加碰撞体

首先要做的是给墙壁添加上碰撞体，限制场景运动区域范围。由于墙壁是静止不动的物体，所以我们给它添加一个 *StaticBody2D* 静态碰撞体节点。你可以直接在 *Sprite* 节点下添加一个静态碰撞体，并设置好碰撞体大小；也可以把 *Sprite* 作为*StaticBody2D* 的子节点，这也是推荐的流程。但是在没有特殊用途下（比如不需要添加代码等），你可以随便安排， Godot 中的节点是非常灵活的。

这里为了正确设置碰撞体的形状，我把之前单一的墙壁背景拆分为了四面独立的墙，然后分别设置碰撞体形状。接着要在玩家节点上添加碰撞体，这里我们需要谨慎操作：**第一是注意节点的类型，和墙壁不同，玩家是可以移动的，且拥有物理属性，所以不能使用静态碰撞体；第二是节点的父子关系的顺序问题，我们因为要移动碰撞体，而不是 Sprite 精灵图片节点，所以 Sprite 应该作为碰撞体节点的子节点，且不能弄反！**详细解说在我的入门文章第二篇中有详述： [Godot3 游戏引擎入门之二：第一个简单的游戏场景](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/09/11/introduction-of-godot-3-part-2-game-scene-and-node/)。

和大名鼎鼎的 [Box2D](https://link.zhihu.com/?target=https%3A//box2d.org/) 开源物理引擎类似， Godot 中也有三种常用的物理碰撞体：*StaticBody2D | RigidBody2D | KinematicBody2D* ，同属于 *PhysicsBody2D* 类型下，它们之间的异同点大致如下；

节点名StaticBody2DRigidBody2DKinematicBody2D节点名称静态碰撞节点（ 2D ）刚体节点（ 2D ）运动学节点（ 2D ）基本特性自动碰撞检测，位置固定不变自动碰撞检测，产生碰撞响应：有线速度、角速度等参与碰撞检测，无自动响应，完全由代码控制移动使用场景一般用于固定的墙壁、地面等一般用于受外界影响而产生运动的物体，比如球体、陨石等主要用于由代码控制的带物理属性的玩家

了解了这三种节点后，得出的结论是不是应该给我们的主角添加一个 *KinematicBody2D*运行学节点呢？嗯……然而并不是，如果使用 *KinematicBody2D* 节点，我们需要自己手动控制物理反馈，虽然绝大多数的游戏应该这样，但是这不是本篇文章的做法，尽量不要动代码是我的出发点，以后再介绍 *KinematicBody2D* 节点，现在我们暂时使用简单一点的 *RigidBody2D* 刚体节点进行尝试。（是不是听上去有点不符合直觉？其实在有些游戏中，比如太空飞船射击游戏，就可以使用 *RigidBody2D* 作为玩家节点进行开发。）

理论到此为止，给我们的游戏场景添加一个 *RigidBody2D* 刚体节点，改名为 *Player*，然后把之前的玩家 *Player* （ *Sprite* ）节点拖到 *RigidBody2D* 节点下作为其子节点，同时 *AnimationPlayer* 节点也要作为刚体节点的子节点，保持和 *Player* 节点平级的关系，最后添加一个 *CollisionShape2D* 节点用于设置碰撞体的形状。

![img](https://pic2.zhimg.com/80/v2-596746f41710582409b64b21312df2b1_720w.jpg)godot_5_rigidbody2d

最终场景中的节点如上图，唯一要设置的是把 *RigidBody2D* 的重力影响属性 *Gravity Scale* 设置为 0 ，即完全摆脱重力的影响，不这么设置的话，你会发现玩家会“情不自禁”地做自由落体运动。另外，值得注意的是，我在改名的过程中，原来的 *Player* 节点自动更名为 *Player1* ，然后动画全部失效，解决办法很简单，在动画面板里把轨道的名字改过来即可，如下图：

![img](https://pic3.zhimg.com/80/v2-4e857435fdcf0e36b2ad6e8c14e466fe_720w.jpg)godot_5_change_node

## 最终代码

场景一切就绪，接下来的任务就是修改代码了！因为我们的节点关系产生了变化，还有节点的行为也变了（ *Sprite* -> *RigidBody2D* ），所以对于新手朋友我要特别提醒的是：**玩家已经转变成 RigidBody2D 刚体节点了，刚体节点是会自动产生物理响应的，所以我们不能像刚才那样直接使用代码操作玩家的位置，相反，我们应该通过设置刚体的线速度、角速度来实现对刚体运动的控制！**

具体修改我都在代码中做了注释，代码量不大，相信大家都能看懂吧。这里全部的代码我就不贴出来了，修改部分如下：

```text
onready var animationPlayer = $Player/AnimationPlayer # 修改后
onready var camera = $Camera2D

player.linear_velocity = velocity # 添加部分，设置线速度，速度为0时有用
player.angular_velocity = 0 # 添加部分，设置角速度，防止player打转
# 速度不为0，移动玩家位置，同时更新摄像机
if velocity.length() > 0:
    # 注意这里normalize速度矢量
    # player.position += velocity.normalized() * speed * delta # 删除
    player.linear_velocity = velocity.normalized() * speed # 添加，更新速度
    # 更新摄像机，玩家始终在视窗内活动
    updateCameraPosition()
    # 省略代码……
```

终于完工，按 *F5* 运行游戏，看看我们的杰作吧：

![img](https://pic4.zhimg.com/v2-8b3a0665f532f7c185469c50708eb6c7_b.jpg)

## 三、小结（下）

相对来说，这篇的知识点还是非常简单的，当然对于编程初学者来说，代码还是一个需要克服的地方。在接下来的文章里，我会针对 2D 游戏中的地图创建做几篇文章，也就是*TileMap* 节点的功能介绍和使用，打造一个游戏该有的丰富世界！

最后，本篇上下节结束后，我要提醒新手朋友们几个注意点：

1. 我们实际项目中使用 RigidBody2D 来作为玩家还是比较少的，相对多的还是 KinematicBody2D 节点
2. 我们对物理碰撞的处理不应该放在 `_process(delta)` 方法中，而应该放在`_physics_process(delta)` 方法中，后续再讲
3. 地图太简单了，这也是这篇要埋下的伏笔，下篇介绍，“等着瞧”，哈哈

**原创实属不易**，希望大家喜欢！ :smile:

# Godot3游戏引擎入门之六：制作TileMap瓦片地图

[![刘庆文](https://pic2.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

24 人赞同了该文章

## 一、前言

收到一个高兴的消息： 2018 年 Github 最新统计出炉， Godot 是所有项目里增长速度最快的第三位！所以，我还是非常看好它的，哈哈！链接在此： [Fastest growing open source projects](https://link.zhihu.com/?target=https%3A//octoverse.github.com/projects) ，截图如下：

![img](https://pic3.zhimg.com/80/v2-ad5d62ca85544130e8ddad6c7cb9f182_720w.jpg)godot_in_github

吹逼结束，本着承上启下的精神，本篇一起来学习并打造一个“美丽壮观”的游戏世界。使用的工具是 Godot 中的 *TileMap* 瓦片地图节点。**注意：本系列文章包括本篇依旧使用** **[Godot 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha1/)讲述故事的经过，但这并不影响学习使用 Godot 3.0 版本中的瓦片地图制作，不过在此我要提醒的是：预览版中** ***TileMap*** **新增了一些强大且实用的功能，这些我会在后面讲解，然后请记得在使用这些新功能的时候，务必时刻保存你的游戏项目，不然有可能因为 Crash 发生奔溃而前功尽弃！嗯，预览版还是有点小 Bug 的， Good luck!**

> 主要内容： Godot 2D 中瓦片地图 *TileMap* 的制作和使用阅读时间： 10 分钟永久链接：[http://liuqingwen.me/blog/2018/10/19/introduction-of-godot-3-part-6-make-tile-map-in-godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/10/19/introduction-of-godot-3-part-6-make-tile-map-in-godot/)系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 了解瓦片地图的一些理论知识
2. 使用图片制作瓦片集 TileSet
3. 使用 SpriteSheet 制作瓦片集 TileSet
4. 介绍 Godot 3.1 中 TileMap 的一些新特性

## TileMap介绍

要打造一个好的 2D 平面游戏，没有一个好的游戏地图，那是万万不行的！你可以没有悦耳的背景音乐，可以没有花哨的粒子特效，没有动人的剧情设计，但是你至少得有一个完整的游戏地图场景来证明你那“伟大”的游戏的存在吧？！在 2D 游戏中，要制作游戏地图相对来时还是很简单的，特别是涉及多个关卡地图，我们通常都是使用 *TileMap* 瓦片地图来实现， *TileMap* 操作简单，效率也高，支持的软件完善，很多游戏都采用它，比如我们小时候耳熟能详的一些“小霸王”游戏：超级玛利亚、坦克大战、魂斗罗等等。

![img](https://pic1.zhimg.com/80/v2-9f92fe144c73c448f7806055444f77e8_720w.jpg)tilemap_games

瓦片地图，简单地说就是一个个瓦片堆积起来的一个地图。如果你有 iOS 游戏开发经验，熟悉 [SpriteKit](https://link.zhihu.com/?target=https%3A//developer.apple.com/spritekit/) 的话，那么你肯定对 *TileMap* 非常了解， [Xcode](https://link.zhihu.com/?target=https%3A//developer.apple.com/xcode/) 对瓦片地图的支持非常完善，功能很强大也易于上手，缺点是 [Xcode](https://link.zhihu.com/?target=https%3A//developer.apple.com/xcode/) 只支持 Mac OS 或者 iOS 系统。另外，熟悉 [Unity3D](https://link.zhihu.com/?target=https%3A//unity3d.com/) 的朋友们也知道，在 *Unity 2018* 版本之前，使用 *Unity*制作 2D 游戏的地图也是很不方便的，如果你想在 Android 或者 Window/Linux 等其他操作系统上开发游戏，那么你需要使用其他的第三方软件来辅助制作地图了。

这里我强烈推荐一款开源软件名为 [Tiled](https://link.zhihu.com/?target=https%3A//www.mapeditor.org/) ，功能非常强大！使用超方便！能很好地支持并导出你设计好的地图到其他游戏引擎中使用，比如配合 [LibGDX](https://link.zhihu.com/?target=https%3A//libgdx.badlogicgames.com/) 框架开发跨平台 2D 游戏。本节的瓦片地图图片就是从 [Tiled](https://link.zhihu.com/?target=https%3A//www.mapeditor.org/) 软件自带的例子中拿过来的，建议大家了解一下这款软件，有兴趣的可以玩一玩，对瓦片地图的制作和了解还是有帮助的。 :smiley:

![img](https://pic2.zhimg.com/80/v2-8128c1506770796535a8ac13de93cd2d_720w.jpg)tiled-screenshot

一个游戏场景就是一个简单的世界，我们可以为这个世界添加很多有趣的元素，让玩家有兴趣去探索，这里我们使用瓦片地图来制作我们的游戏场景，实际上，它是由很多小瓦片组成，当然，完全可以根据情况再添加一些背景，这些小瓦片我们称之为： *Tile* 。瓦片可以很简单，也可以非常复杂，但是在同一个游戏世界里其大小都是统一的，瓦片的类型主要有三种类型： 90° 直角俯视地图（ *Orthogonal/Square* ）、45° 等距斜视地图（ *Isometric* ）、等六边形地图（ *Hexagonal* ）。这三种类型在 Godot 中都是支持的，本篇文章我们主要讨论第一种类型，也是最常用的一种类型吧。 :grin:

## 制作TileSet

理论到此结束，撸起袖子开始干起！要打造瓦片地图，我们首先需要准备好所有的瓦片——也就是所谓的 *TileSet* 瓦片集。在 Godot 中制作瓦片集是非常简单的，我这里介绍常用的两种方式，以及第三种：利用 Godot 3.1 中瓦片地图新特性快速打造自动瓦片地图集！

**第一种方式：使用单独的图片制作瓦片**

第一种方式算是比较古老的一种方法了，在图片数量比较少的时候我们可以选择这种方式，快捷又方便。首先我们需要准备一些相同大小的图片：

![img](https://pic4.zhimg.com/80/v2-98a5a253362858433248a2443a2ba83f_720w.jpg)godot_6_images_folder

接下来，我们需要把所有图片制作成一个一个的 *Sprite* 精灵节点，这些节点最好是放在一个单独的游戏场景中，方便我们日后编辑。这里我单独创建一个名为*TileSet_Sprites* 的游戏场景，然后把所有瓦片图片资源直接拖拽到场景中，并选择*Sprite* 方式创建所有的节点。接着使用 Godot 菜单直接把场景中的所有 *Sprite* 节点转化为瓦片，制作 *TileSet* 瓦片集资源。在菜单栏中依次选中： *Scene -> Convert To -> TileSet* ，选择项目中某个位置保存资源为 `tileset_sprits.tres` ，一键完成制作我们所需要的瓦片集，既简单又快捷！

![img](https://pic3.zhimg.com/80/v2-b409800cf617a4a9cde3c0a7d1f5f02e_720w.jpg)godot_6_convert_tileset

瓦片集准备好了，下一步就是使用它来制作你那伟大的游戏地图了！我们制作地图的节点叫做 *TileMap* 瓦片地图，使用也很简单，只要把 *TileSet* 资源添加到 *TileMap* 即可。首先创建一个主场景，在根目录下添加一个 *TileMap* 地图节点，注意，这里一定要设置好**地图的单元尺寸**，即 *Cell* 属性，示例中瓦片尺寸都是 *32x32* 像素，所以按此设置即可。接着在 *Tile Set* 属性菜单下点击 *Load* 加载我们刚才制作完的瓦片集资源`tileset_sprits.tres` ，这时你会看到所有的小瓦片都出现在编辑器中了，选中任意一个瓦片，开始你的艺术创作吧，骚年！ :sunglasses:

![img](https://pic2.zhimg.com/80/v2-cc7d29715dad14e1bac3c96dce966cd9_720w.jpg)godot_6_load_tileset

**第二种方式：使用图片合集制作瓦片**

当我们制作的地图元素非常多的时候，第一种方式明显不合常理了！图片过多导致文件难以管理，加载性能也会下降，这时候我们一般会把图片制作成 *SpriteSheet* 图片精灵集，这样既能减少文件数量，方便管理，又能提高加载速度和游戏的性能，关于*SpriteSheet* 的原理我推荐大家到 [TexturePacker](https://link.zhihu.com/?target=https%3A//www.codeandweb.com/) 软件官网上浏览开发者的相关文章： [What is a sprite sheet?](https://link.zhihu.com/?target=https%3A//www.codeandweb.com/what-is-a-sprite-sheet) ，这篇文章图文详细介绍了什么是 *SpriteSheet* ，以及它的优势和原理。

除了图片资源形式不同，其他原理和第一种方式并没有什么不一样：我们把单张*SpriteSheet* 图片转化为一个一个的 *Sprite* 节点，然后一键转换为 *TileSet* 资源就可以了。理论如此，但在操作过程中会有一个问题：一张大图由很多的小图拼成，这些小图需要制作成一个个的 *Sprite* 节点，那么如何精确的把这张大图划分为大小统一的小图呢？这样做工作量岂不是比第一种方式要大很多？——别急， Godot 肯定想到这点了，既然大小统一，我们只需要开启 *Snap* 吸附功能就可以轻松完成区域划分了！具体操作在场景窗口的上方菜单栏选项里，打开吸附功能，并设置相关参数，然后就可以精确地进行相关操作了：

![img](https://pic1.zhimg.com/80/v2-11d3f1473731ae70361fa59b49e16454_720w.jpg)godot_6_snap_setting

停！！！貌似这并没有什么卵用啊？是的，这个吸附功能只在场景编辑操作中适用，和我们现在要制作的精灵节点并没有半毛钱关系，不过原理是一样的。创建一个 *Sprite* 节点，把 *SpriteSheet* 大图拖拽到 *Texture* 属性下，然后勾选开启 *Region* 特性，打开 *TextureRegion* 编辑工具窗口，吸附功能就在这个窗口中进行设置。注意：我所使用的这张图的每一个小图片都有偏移，偏移像素为 1 个像素，所以需要在 *Grid Snap* 网格吸附选项里进行相关设置。具体操作如下动图：

![img](https://pic4.zhimg.com/v2-454f88b2841021f905582f621561bc6b_b.jpg)

虽然我只操作了两张图，不过还是蛮快的，只要按住 *Ctrl + D* 复制一下节点，利用吸附功能框选一下 *Sprite* 的材质区域即可，付出一点耐心，很快就能把所有节点制作完成，最后和第一种方式一样，一键把场景转化为 *TileSet* 资源。在游戏主场景中，再创建一个新的地图，隐藏刚才的创建的地图，选择我们新建的 *TileSet* 资源进行地图绘画，效果如下，注意我框选的几个角落：

![img](https://pic2.zhimg.com/80/v2-6ac72de1a23c292e511bebc8e12a0af5_720w.jpg)godot_6_tilemap_painting

**第三种方式：新版本中瓦片地图新特性**

终于轮到新版本中的地图新特性了！这种方式最为方便，也是功能最强大的一种方式，操作流程也与上面两种方式截然不同。再次提醒一下：**在使用 Godot 3.1 预览版中的 TileMap 新功能的时候，务必时刻保存你的游戏项目，因为预览版还不够稳定，有可能会产生意想不到的奔溃，牢记牢记！**

第一步，使用瓦片地图之前，我们需要手动创建一个空的 *TileSet* 资源，并保存到合适位置：

![img](https://pic2.zhimg.com/80/v2-6a2a3baefbc68e55ae6d010a1b294d8d_720w.jpg)godot_6_create_resource

记住，这种方式同样适用于其他资源的创建。第二步就是愉快地使用 Godot 3.1 版本中的地图新特性了，使用新功能快捷创建一个强大的**自动地图集**。啥叫*自动地图集*？参考上面的那张效果图，注意几个角落，所谓的自动地图集，顾名思义就是画地图的时候不需要手动去添加那八个角落了， Godot 自动帮我们完成，是不是很方便？

![img](https://pic4.zhimg.com/v2-003782bd0f65e8305bc08fef91c8fe87_b.jpg)

godot_6_autotile

如果上图看不清可以查看大图： [Godot 3.1 自动地图集操作详细动图](https://link.zhihu.com/?target=http%3A//godot_6_autotile_1350x982.gif/)。另外，*TileMap* 新特性中的有些功能是我们没见过的，比如，我们制作 *TileSet* 范围就是勾画*Region* 区域，而 *Bitmask* 区域则是告诉 *TileMap* 如何自动完成整片地图的绘制，*Priority* 代表图片出现的概率， *Icon* 用来设置自动地图图标，还有我们后续游戏场景中会使用到的碰撞功能： *Collision* 碰撞区域设置，详细说明我在下图中都勾选出来了。总之，这么多新特性，大家可以多做一些尝试。 :smile:

![img](https://pic4.zhimg.com/80/v2-757815e73f8b975a6b0db81bc36578bf_720w.jpg)godot_6_new_tilemap_tools

## 其他说明

这里我们只是简单地尝试了一下 Godot 中的瓦片地图制作，后续有机会我还会介绍如何在瓦片地图上添加一些其他物理特性，比如光照遮挡，或者添加真正的碰撞体，以实现游戏世界中的墙壁、地面等。

最后， Godot 3.1 中还有一个辅助小特性，可以设置瓦片集合 *Atlas* ，即一组瓦片组成一个集合，方便地图绘制，如下图：

![img](https://pic3.zhimg.com/80/v2-c4c43d1f4f1541a28db83e6df896339a_720w.jpg)godot_6_atlas_tiles

附加知识：关于旧版本 Godot 中的瓦片地图绘制，如果不熟悉可以先看看 [Xcode](https://link.zhihu.com/?target=https%3A//developer.apple.com/xcode/) 中的关于瓦片地图的一些标记：

![img](https://pic3.zhimg.com/80/v2-30bb1203c75eddacecba09eb87009cf6_720w.jpg)tile_terrain

这里有一个例子，如何画一片海洋区域：

![img](https://pic3.zhimg.com/80/v2-8c9a6607d192243c588a69168ef7e83a_720w.jpg)tile_terrain_explain

## 三、小结

本篇就这样利用多图完成了，不知道读者朋友们看完有啥感想？如果你能坚持从我的 Godot 系列第一篇文章读到本篇文章，那么非常感谢你的阅读，其实我最近更新的速度越来越慢，写完一篇文章至少要耗费我 3 天的闲暇时间，这篇文章更是花费了我一周，因为平时要工作，闲余时间还不一定有空，所以，等待更新的朋友要耐心点了。读完，我相信你应该会和我感受一样： Godot 必定能火！哈哈！最后，附上 InfoQ 中关于 Github 的最新统计信息报告： [GitHub发布史上最大更新，年度报告出炉！](https://link.zhihu.com/?target=https%3A//mp.weixin.qq.com/s/ccEYMl2_0QZ5B5VHSqDXLA)

**原创实属不易**，希望大家喜欢！ :smile:



# Godot3游戏引擎入门之七：地图添加碰撞体制作封闭的游戏世界

[![刘庆文](https://pic2.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

8 人赞同了该文章

## 一、前言

在前面的文章中，我分别介绍了如何上下左右移动玩家，以及使用瓦片集制作丰富的游戏地图，现在，是时候结合在一起，制作一个简单的游戏世界了，这个游戏世界既有丰富的场景元素，也有合理的碰撞检测，玩家可以在封闭的世界里自由移动。



[刘庆文：Godot3游戏引擎入门之五：上下左右移动动画（下）9 赞同 · 0 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/46788570)

[刘庆文：Godot3游戏引擎入门之六：制作TileMap瓦片地图24 赞同 · 2 评论文章![img](https://pic3.zhimg.com/v2-b293558884dcd33b387bc36b2b3fefc6_180x120.jpg)](https://zhuanlan.zhihu.com/p/47222109)

上面的第一篇文章中，其实我们已经实现了一个简单的封闭世界，我们是这样实现碰撞检测的：给场景中的墙壁添加静态碰撞体，给玩家节点添加 *RigidBody2D* 刚体属性，我们在代码中设置玩家的线速度，而大部分物理属性由 Godot 引擎帮我们实现了。在第二篇文章中，我们又通过学习 *TileSet* 和 *TileMap* 可以在游戏中制作出复杂的场景，但问题是：地图上还缺少碰撞体，无法和玩家进行交互。

所以，这篇文章要解决上面两个小问题：第一，使用 *KinematicBody2D* 节点作为玩家对象，这样我们能自由控制物理反馈，实现相关的游戏功能；第二，我们需要给地图添加更多的真实的碰撞体，比如墙壁、障碍物等。这也是我们游戏开发的正常流程。

> 主要内容： 给 TileMap 地图添加碰撞体并测试
> 阅读时间： 4-6 分钟
> 永久链接：[http://liuqingwen.me/blog/2018/10/22/introduction-of-godot-3-part-7-add-collision-and-move-player-in-map/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/10/22/introduction-of-godot-3-part-7-add-collision-and-move-player-in-map/)
> 系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 给地图中的瓦片添加碰撞体
2. 玩家添加碰撞体，在地图中移动测试
3. 学习几个实用的脚本函数

## 添加碰撞体

在[上篇文章](https://zhuanlan.zhihu.com/p/47222109)的基础上，我们需要给每一个瓦片添加上碰撞体，这个操作很简单，直接添加具有碰撞体功能的节点即可。在 Godot 3.1 新版本中，设置步骤稍微繁琐，但是效果更加直观，效率也会更高。两种方式我们都了解一下，具体操作方式可以根据你的 Godot 版本而定。

**3.0 版本**

首先打开我们之前保存过的用于创建 *TileSet* 资源的游戏场景文件（`Tileset_Sprites.tscn` 和 `Tileset_SpriteSheet.tscn` ），然后直接给每一个节点添加碰撞体。场景中的 *Sprite* 节点最终都会转化为 *Tile* 瓦片，要给每个瓦片添加碰撞体，只需要在每个 *Sprite* 节点下添加一个 *StaticBody2D* 静态碰撞体作为子节点，然后给静态碰撞体添加 *CollisionShape2D* 节点并设置碰撞体形状即可。

![img](https://pic3.zhimg.com/80/v2-d081e77f8439d1125f457a09328a9caa_720w.jpg)godot_7_add_collision_node

这些都在前面的文章里已经详细介绍过了，不过要特别注意的是：给所有 *Sprite* 节点都添加了碰撞体后，必须**重新保存**以覆盖之前的 *TileSet* 资源，才能把碰撞体更新到地图中，否则设置了碰撞体也不会有效果。文章后面我会介绍 Godot 中强大的 *Debug* 功能对碰撞体进行可视化测试，避免意外情况。

**3.1 版本**

Godot 3.1 新版本关于 *TileMap* 的一些新特性[上一篇文章](https://zhuanlan.zhihu.com/p/47222109)已经介绍过了，基本流程类似：*划分 Region 区域 -> 标记 Bitmask 掩码 -> 添加 Collision 碰撞体区域*。新版本不需要添加任何子节点，直接在相应的瓦片上绘制碰撞体形状即可。如下图，相关参数[上一篇文章](https://zhuanlan.zhihu.com/p/47222109)已经介绍过了：

![img](https://pic4.zhimg.com/80/v2-2781b89a04c20d2511856a7b370fcf57_720w.jpg)godot_7_tilemap_collision

> 注：黄色代表已绘制的碰撞体，蓝色代表正在绘制的碰撞体。操作提示：如果不方便设置自动吸附的参数，那么在绘制碰撞体形状的时候会出现很难精确点位的问题，这个时候我们可以取消吸附，选择粗略绘制完的碰撞体，点击*Points* 属性值，对每一个点进行手动修改调整即可。

一般我们给墙壁和不可穿越物体设置碰撞体即可。设置完每一个瓦片集的碰撞体形状后，地图上就会出现相应的**静态**碰撞体了，新版本操作起来非常简单快捷！

## 添加主角

游戏世界里怎么能缺少玩家呢？老生常谈的话题，前面的文章已经多次介绍如何制作完整的 *Player* 玩家节点了，这里我们的地图是支持 *Player* 上下左右移动的，实现起来也不难，具体请参考上一篇文章的详细介绍：[Godot3 游戏引擎入门之五：上下左右移动动画（下）](https://zhuanlan.zhihu.com/p/46788570)。本次我们的主角 *Player* 主要有两种状态：静止（ `idle` ）和跑动（`run` ），注意设置动画的总时长和开启循环播放。另外，由于原图稍大，不能直接放在地图中，我对玩家 *Sprite* 节点进行了缩放。

![img](https://pic3.zhimg.com/80/v2-7db99ac0d64c94379ca7bf4257500506_720w.jpg)knight

**说明：和前面几篇文章不同的是，这里我使用了游戏中常用于制作玩家根节点的 KinematicBody2D 图形学节点作为 Player 对象的根节点，并添加一个 CollisionShape2D 节点作为碰撞体。**这样做既能让 *Player* 参与物理响应，又能在代码中操作其移动。

![img](https://pic4.zhimg.com/80/v2-25c50d9e5c520ba260f6c1fd3b7a8a17_720w.jpg)godot_7_collision_shape_size

另外有三个需要注意的地方：

- 第一个是碰撞体形状中的 `Extends` 属性值表示半宽和半高，这和 [Box2D](https://link.zhihu.com/?target=https%3A//box2d.org/)物理引擎一样
- 第二个是我们设置的碰撞体形状要比图片稍小，这样能防止意外碰撞，产生不必要的碰撞运算和效果
- 第三个，也是非常重要的一点：**不要缩放碰撞体形状**，即：不要设置`scale` 属性

第三点同样是为了防止产生意外碰撞情形，不过这点貌似在 Godot 3.1 版本中已经修正了：在绘制碰撞体图形时不能直接拖拽鼠标进行缩放碰撞体了：

![img](https://pic1.zhimg.com/80/v2-6bf4eb60af4965d8098e5ecd4cf12864_720w.jpg)godot_7_handle_of_collision_shape

准备工作已经完成，接下来就是最关键的部分：脚本代码了。

## 编写代码

给游戏场景的根节点 *Game* 添加一个 GDScript 脚本，参考前面学习到的知识， 代码量并不多，新的方法已经做了注释，全部的代码如下：

```text
extends Node2D

# export使变量能在属性窗口中显示和设置值
export(float) var speed = 1
onready var player = $Player
onready var sprite = $Player/Sprite
onready var animationPlayer = $Player/AnimationPlayer

# 在这里不使用_process(delta)方法处理物理引擎，
# 而应该使用_physics_process(delta)方法进行处理
func _physics_process(delta):
    var velocity = Vector2()
    var isMoving = false
    
    if Input.is_action_pressed('ui_left'):
        velocity.x += -1
        sprite.flip_h = true
        isMoving = true
    if Input.is_action_pressed('ui_right'):
        velocity.x += 1
        sprite.flip_h = false
        isMoving = true
    if Input.is_action_pressed('ui_up'):
        velocity.y += -1
        isMoving = true
    if Input.is_action_pressed('ui_down'):
        velocity.y += 1
        isMoving = true
        
    if velocity.length() > 0:
        velocity = velocity.normalized() * speed
        # 关键代码：移动并测试碰撞体，参数为玩家的移动速度
        player.move_and_collide(velocity)
    
    if isMoving and animationPlayer.current_animation != 'run':
        animationPlayer.current_animation = 'run'
    elif ! isMoving and animationPlayer.current_animation != 'idle':
        animationPlayer.current_animation = 'idle'
```

新的关键词和脚本函数介绍；

1. `export` 关键字修饰的变量能在编辑器的属性窗口中显示并设置值，类似 Unity 中的 `public/[Serialized]` 关键词
2. `flip_h` 布尔值表示图片是否**水平翻转**，产生向左或者向右的效果，相比使用 `scale` 缩放属性更加方便简洁
3. `move_and_collide(Vector2)` 这是本文 Demo 代码的精髓部分，传递一个**速度矢量**参数，游戏引擎将移动并处理物理碰撞，简洁又强大

![img](https://pic4.zhimg.com/80/v2-5f8b68c76107cdb36b3f2a80e5526c97_720w.jpg)godot_7_export_variable

## 效果调试

全部完成了，按 *F5* 运行游戏，测试我们的最终成果吧。感觉如何？反正我还是有点激动的，“尽情”探索一个“未知世界”吧：有围墙，有障碍物，有墙壁，各种地形等，如果在跑动过程发现有任何问题，别慌，你还可以对地图的所有碰撞体进行 Debug 调试！这也是 Godot 的强大功能之一，在 Debug 菜单下勾选 *Visible Collision Shapes* 选项即可开启！

![img](https://pic3.zhimg.com/80/v2-9299051efe57c451a6ab46320616d04e_720w.jpg)godot_7_debug_collision

开启碰撞调试后运行游戏的效果：

![img](https://pic2.zhimg.com/v2-62092d17791914ebae421683d7086079_b.jpg)

注意图中的蓝色形状体就是地图碰撞体，是不是和预期一样？调试的时候，我稍微放大了*Player* 节点图片，测试的时候看得清楚些，如果你之前有多余的地图，那么场景中可能有多余的不可见的碰撞体存在，这样会影响游戏运行，避免的方法可以直接删除之前的*TileMap* 测试地图，也可以在瓦片地图属性下对碰撞图层进行设置，取消碰撞图层和碰撞掩码即可，关于碰撞图层和掩码设置我在后面再讲，操作如下图：

![img](https://pic2.zhimg.com/80/v2-80516d5ec3e3a04ffb56495e4497856d_720w.jpg)godot_7_set_collision_layer

确认场景没有问题后，关闭调试，运行游戏，享受一下自己的成果吧！ :smiley:

![img](https://pic2.zhimg.com/v2-07cd11fc0836f081a09ee3bdfe1cce3d_b.jpg)

## 三、总结

本篇文章可以算是之前文章的一个结合，是不是感觉越来越简单了？开始动手实现自己的小游戏吧，骚年！不吹逼了，总结下本篇的知识点：

1. Tile 瓦片碰撞体设置
2. Debug 调试地图、玩家的碰撞体运行状态
3. 几个有用的 GDScript 脚本代码技巧

我想，接下来给大家介绍一些游戏开发中常用的、实用的技巧，以及帮助大家提高效率，在强大开源的 Godot 游戏引擎中以正确的姿势开发 2D 小游戏！“静候佳音”吧，哈哈。嗯，还是那句话，**原创不易**，希望大家喜欢！ :smile:



# Godot3游戏引擎入门之八：添加可收集元素和子场景

[![刘庆文](https://pic1.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

4 人赞同了该文章



## 一、前言

在前面的游戏地图基础上，我们已经实现了玩家的上下移动控制，也有了相应的碰撞体功能，一个小小的游戏世界已经打造好，不过对于一个完整的游戏来说还是缺少点什么，没有探索的乐趣就没有吸引力，因此，这也就是我们本篇要实现的目标——给游戏场景添加一些可爱的动画元素，比如金币，来供玩家探索吧！

除此之外，我还会介绍 Godot 中两个非常重要的概念或者实用技巧：子场景的创建和 Godot 中信号的使用。和之前的文章一样，本篇也是基于上一篇文章：

[刘庆文：Godot3游戏引擎入门之七：地图添加碰撞体制作封闭的游戏世界8 赞同 · 4 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/47481382)



> 主要内容： 在游戏场景中添加互动元素
> 阅读时间： 10 分钟
> 永久链接：[http://liuqingwen.me/blog/2018/11/02/introduction-of-godot-3-part-8-add-collectable-elements-and-sub-scenes/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/11/02/introduction-of-godot-3-part-8-add-collectable-elements-and-sub-scenes/)
> 系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 创建子场景，实例化，并添加多个子场景
2. 介绍 Area2D 节点的功能和应用
3. Godot 中的观察者模式实现：信号的使用
4. 创建和使用包含函数调用的复杂动画

## 创建玩家子场景

为什么需要**子场景**呢？这其实有点类似程序中的**面向对象思想**，如果你有使用 Unity 开发游戏的经验，那么你对 Unity 中深入人心的 [Prefab](https://link.zhihu.com/?target=https%3A//docs.unity3d.com/Manual/Prefabs.html) 预制体概念肯定非常熟悉；同样地在 Apple 中开发 *2D* 游戏，使用 [SpriteKit](https://link.zhihu.com/?target=https%3A//developer.apple.com/spritekit/) 也会创建很多的子场景： *SKScene* ，然后在主游戏中加以重复利用。 Godot 中也有类似的概念，想象一下，当你需要在场景中制作很多个功能类似的物体，比如多个相同的敌人，每个场景中数量还不一定一样，如果每个场景中都去单独制作一个个的敌人对象，那就显得*非常地不优雅*了，万一设计不合理，全部都需要修改呢？这个时候，你就可以把它制作成一个**预制件**，使用预制件来克隆多个敌人，当你需要修改某个功能的时候，你只需要修改这个**预制件**，那么所有的实例都能得到应用，方便高效，还能提高游戏性能。这就是 Godot 中所谓的 *Sub-Scene* 子场景概念了。

说的很多，实际上做起来很简单。首先，我又得做下比较了： Godot 中的子场景可比 Unity 中的预制体功能强大多了！子场景可以嵌套，可以覆盖，甚至还能单独运行，非常方便。其次，我们要了解到，什么情况下需要子场景：第一，独立的节点可以制作成子场景，方便开发、调试、合作；第二，重复利用的元素可以制作成子场景。最后，我们来使用子场景来改进一下我们当前的游戏结构。

在我们的游戏主场景中，玩家 *Player* 是一个*五脏俱全*的子节点，这里我们完全可以把它当做一个单独的场景进行开发利用，这样的好处在于可以单独修改 *Player* 节点，提高效率，而且当你有需求要在游戏的主场景中添加多个玩家的时候（这里不太可能，不过以后我们再谈多玩家局域网连线游戏），你会发现特别地方便！制作子场景一般有两种方式，这两种方式都非常简单，灵活采用。

我们先讲第一种方式：把场景中已有的节点转化为子场景。在我们的游戏主场景中，选择*Player* 玩家节点，右键弹出菜单中，选择 *Save Branch As Scene* 即把该节点转化为场景，然后选择合适的位置，保存即可！现在 *Player* 节点变成了一个*单独的子节点*了，右边的 电影小标志说明该节点为一个子场景，你可以通过点击这个标志进入*Player* 子场景进行编辑，非常简便、贴心。

![img](https://pic3.zhimg.com/80/v2-11c472d12f7e35b2206b26e962c8f7fe_720w.jpg)godot_8_subscene.jpg

前面说过，子场景类似预制体，可以进行克隆创建出多个子场景的实例，接下来我们就通过制作金币子场景对此进行讨论。

## 制作金币场景

我们创建一些**金币**来丰富游戏的场景，供玩家探索发现。先构思一下金币在游戏世界中的表现：有一个金币，它闪耀在世界的某个角落，如果有幸被玩家拾取，将会播放一段动画，然后消失于人间！嗯，是时候把我们的想象力转化为实际操作了：我们来创建一个单独的金币子场景，包含有两个动画，一个是闪耀，另一个是消失动画，还要有碰撞反馈，最好能自我消失！ :grin:

这就是我要讲的第二种子场景制作方式，首先我们点击场景编辑器上方的 *+* 号按钮，创建一个单独的场景，选择什么节点作为金币场景根节点呢？这里我要介绍一个新的节点：*Area2D* 区域节点。为什么要使用 *Area2D* 节点而非普通的 *Node2D* 或者之前我们多次接触过的具有碰撞属性的 *StaticBody2D/KinematicBody2D* 节点呢？原因在此：我们只需要一个能检测碰撞，但不需要有任何物理反馈的节点。 *Area2D* 在此非常合适，它可以用来制作一个区域，检测玩家进出该区域，相比 *PhysicsBody2D* 下的物理碰撞属性节点，它没有质量、弹性等属性，所以性能更高，另外有了 *Area2D* 作为根节点，我们没必要使用 *Node2D* 节点了。

选择 *Area2D* 作为根节点，改名为 *Coin* ，然后添加碰撞区域节点和图片、动画节点，调整相应设置，按 *Ctrl+S* 保存为 `Coin.tscn` 场景资源，场景结果如下图：

![img](https://pic2.zhimg.com/80/v2-f50ba3220d64ae5730822c740854a6b1_720w.jpg)godot_8_new_scene.jpg

接下来需要给金币制作动画，按照前面的分析，需要两个动画：一个是没有被收集时的闪耀状态，一个是被收集后立刻消失的动画。第一个动画 `rotate` 非常简单，对于第二个消失动画 `disappear` 则稍微复杂点，但是只要把动画思路弄清楚，然后分多个轨道单独进行设计，调整，做出好看的效果也就非常简单了，动画分多个轨道：

- 碰撞体禁用属性：玩家收集金币后碰撞体不再有效，启用 `disabled` 属性
- 金币位置属性：金币从下往上漂浮，即 `position` 位置属性
- 透明度属性：在颜色属性里让透明度变为 `0` ，即 `modulate` 中的`alpha` 值
- 缩放属性：再添加一个缩放动画，在位置变化过程中不断缩小，即 `scale`的值
- 最后一个，金币需要回到第一帧，防止以某个侧面图片进行消失，设置`frame` 为 `0` 即可

![img](https://pic4.zhimg.com/80/v2-0a48c80f06324d5f1405f0482e2bb58b_720w.jpg)godot_8_coin_animation.jpg

记得做动画过程中不断测试和调整播放时间。是不是感觉 Godot 中的*AnimationPlayer* 简直是太强大了？嗯，甚至有点像 Adobe Animate （ Adobe Flash ）动画工具啦！最后，提醒一点：由于金币会在玩家碰撞后立刻进行消失动画，这个时候我们要保证玩家不会再和金币继续产生二次碰撞，所以一定要在消失动画的第一帧就禁用碰撞体，同时注意运行游戏之前**别因误勾选而禁用了碰撞体**，这点特别重要，如果不明白怎么回事，又发生了金币不能被正常收集，那么你可以参考我之前的文章，使用 Godot 的碰撞体调试功能测试一下吧！ :sunglasses:

## 连接信号

我们的场景已经准备完毕，现在需要添加一些操作来实现游戏的运行逻辑了。首先我们要做的是：当金币检测到与玩家有碰撞响应后立刻播放消失动画，表明已被收集。这个碰撞相当于一个触发器，而这个触发器在 Godot 中就是以 *Signal* 信号的方式传播出去的，我们收到信号之后立刻更改动画就可以了。那么，问题来了，这里涉及到一个非常重要的概念： *Signal* 信号，这又是什么鬼？别急，且听我慢慢解释。 :smiley:

编写过程序的朋友应该对程序设计模式中的**观察者模式**或多或少有所了解，观察者模式听上去很专业，高大上，实际上原理非常简单：有一个物体叫做事件源，也可叫*被观察者*，另外有一个物体叫订阅者，也叫*观察者*，或者*事件侦听者*，观察者订阅事件源的某个事件，当事件源发生了这个事件后，它并不需要知道谁订阅了它，只管把事件广播出去即可，然后那些订阅了这个事件的观察者们就能立刻侦听到这个事件，做出相应的处理，这就是所谓的**观察者模式**。

举个例子，想象一下有这么几个主角：某指挥中心、某急救中心和某狙击手。他们之间的关系和事件，如下：

- 狙击手作为*被观察者*，可随时发报
- 指挥中心作为*观察者*，时刻等待*信号*到来
- 急救中心同样*订阅*了狙击手的事件，作为*观察者*
- 狙击手发现敌人，*发出信号*：“大量敌人出现”
- 指挥中心收到*信号*，做出反应，立即派遣救援
- 急救中心并*没有订阅*这个事件，或者*订阅*了也不处理
- 狙击手被敌人干掉，*发出信号*：“ Help me! ”
- 急救中心*订阅了该事件*，马上行动，开始救援

这就是观察者模式，如果还不清楚的话，可以看下图：

<iframe title="video" src="https://video.zhihu.com/video/1042002902834970624?player=%7B%22autoplay%22%3Afalse%2C%22shouldShowPageFullScreenButton%22%3Atrue%7D" allowfullscreen="" frameborder="0" class="css-uwwqev" style="width: 688px; height: 387px;"></iframe>

0:10 Godot观察者模式-Signal信

理解了观察者模式，就理解了 Godot 中的信号，回到金币场景中，当 *Area2D* （ *Coin*） 发生碰撞的时候，立刻发出“碰撞”信号，所有的“感兴趣的订阅者”收到这个信号后作出各自相应的处理，这个处理就是订阅者们的“某个函数”。在 Godot 中订阅事件或者信号叫 *Connect* 连接，信号发出后，连接了该信号的订阅者的相应函数会被调用，也就是成功处理了该事件，完成一个流程。如何使用 *Signal* 信号呢？原理简单，操作也不难：

![img](https://pic3.zhimg.com/80/v2-782e73b6d46fa14577a6032dda616d86_720w.jpg)godot_8_connect_signal.png

按上图中的操作步骤：先给 *Area2D* （ *Coin* ）添加一个空脚本，然后点击发出信号的节点 *Area2D* （ *Coin* ），在 Node 面板的 Signals 下显示了 *Area2D* 节点的所有信号种类，这里我们选择 `body_entered(PhysicsBody2D body)` 也就是**碰撞体进入**信号，双击它或者单击右下方的 *Connect...* 按钮，在弹出框中选择接收该信号的订阅者（这里订阅者仍然是金币节点本身，自己处理自己发出的信号），设置处理信号的方法函数，注意 *Make Function* 默认开启，如果关闭了则需要在脚本中手动编写该函数！连接后我们打开脚本文件，可以看到 Godot 自动帮我们添加了一个方法，同时在*Area2D* 的信号面板中也有了变化： `body_entered(PhysicsBody2D body)` 信号下有了新建方法的连接提示。啰嗦了点，图片能理解的朋友直接跳过吧！

暂时丢下代码，我们转到主场景中添加我们制作好的金币子场景。在主场景中，点击 链接按钮，然后选择我们保存的金币场景资源 `Coin.tscn` 文件，即可实例化一个金币到主场景中，重复这个操作，多添加几个金币，放置到不同的位置，充分发挥你的想象吧！

![img](https://pic3.zhimg.com/80/v2-0ea2d34f60c8271b6f9c674cf4715842_720w.jpg)godot_8_instance_subscene.jpg

工作基本完成，第二种子场景制作方式也介绍了，信号的原理、使用、添加也了解清楚了，最后就是逻辑处理啦。

## 逻辑代码

回到金币子场景，打开 GDScript 脚本，添加代码：

```text
extends Area2D

func _on_Coin_body_entered(body):
    $AnimationPlayer.current_animation = 'disappear'
    # 打印文字到控制台，作为测试用
    print('Coin collected!')
```

代码再简单不过！当金币被玩家收集后，也就是发生碰撞的时刻，金币发出信号，在代码中处理信号让金币消失——运行消失动画。运行游戏，测试！

貌似一切 OK ，实际上这里潜伏了一个大问题：硬币被收集后虽然表面上看不见，但实际上并没从场景中消失！如果你开启碰撞体调试就能清楚地看到这个问题的存在，这可能会引起一个运行 Bug ：如果金币一直存在，游戏占用内存越来越多不能及时释放，以至于可能发生内存溢出而导致游戏崩溃！如何处理呢？会不会添加很多逻辑？哈哈，完全没必要，只需再添加一个简单的信号函数就可以轻松搞定！

我们已经在上一节做到了金币收集这个动作，接下来要处理的事情是：当金币的消失动画运行到最后一帧，要把它从游戏中真正的移除！这有涉及到信号的处理，当*AnimationPlayer* 播放到**最后一帧**的时候也会发出一个信号：`animation_finished(String anim_name)` 动画结束事件，和 *Area2D* 的碰撞事件类似，选择 *AnimationPlayer* 节点下的相应信号，把这个信号连接到金币根节点 *Coin*上，在方法处理中把该金币从游戏场景中移除！

```text
extends Area2D

func _on_Coin_body_entered(body):
    $AnimationPlayer.current_animation = 'disappear'
    print('Coin collected!')

func _on_AnimationPlayer_animation_finished(anim_name):
    if anim_name == 'disappear':
        # queue_free方法将出该节点
        self.queue_free()
```

唯一要注意的地方在于代码中的一个判断条件： `if anim_name == 'disappear'` ，这是因为其他动画播放结束的时候也会发出该信号，而我们只想在消失动画结束时候做相应处理。

大功告成，运行查看效果！

![img](https://pic1.zhimg.com/v2-f4ce933c232d1e15adf68cc64d2e8f24_b.jpg)

## Bonus: 函数动画

嗯，并没有结束，学无止境！我们再学习一个 Godot 中动画节点 *AnimationPlayer* 的新特性：函数调用关键帧！试想一下，如果我们可以在消失动画 `disappear` 的最后一帧自动调用金币根节点的 `queue_free()` 方法，那么不就可以实现场景中删除金币而无需连接信号、编写方法、处理逻辑了吗？ Godot 3.1 就是这么强大，如你所愿！

首先，我们为了不重复处理同一个事件，我们需要取消动画播放结束的信号。只需要在已连接好的信号下方，点击 `Disconnect` 按钮取消关联即可。

![img](https://pic1.zhimg.com/80/v2-394012e0ef5e80b6c83cfc6be6349270_720w.jpg)godot_8_disconnect_signal.png

其次，需要稍微修改消失动画。在动画面板中，插入一个新的轨道： *Call Method Track* 即方法调用轨道，然后选择目标为 *Coin* 根节点；创建轨道后，在动画的最后插入一个新的关键帧，弹出 *Select Method* 方法选择框；搜索 `void queue_free()`方法，在 *Node* 类下，点击确定，完成方法关键帧！大致步骤如下图：

![img](https://pic3.zhimg.com/80/v2-ba26d2a5bd754a4d7dd0756d7e2baac6_720w.jpg)godot_8_animation_with_function.png

OK ，总算结束了，高高兴兴地去全世界收集金币吧，骚年！ :sunglasses:

## 三、总结

本章文字偏多，内容并不多，主要介绍了 Godot 中的两个关键特性，希望大家能理解并应用到自己的小游戏中。本篇代码已经上传到 [Github](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos/tree/v0.3) ，最后总结一下本次学习到的知识点：

1. 创建子场景并实例化子场景
2. 连接订阅事件信号，处理信号
3. 学习使用 Godot 3.1 动画中的方法调用特性
4. 其他： Area2D 节点简介，碰撞处理，多轨道动画设计

够啰嗦了，还是那句话，**原创实属不易**，希望大家喜欢！ :smile:


**PS: 图片有一个单词写错 disappear -> disapear ，已经在源代码中更改，注意注意。 :smiley:**



# Godot3游戏引擎入门之九：创建UI界面并添加背景音乐

[![刘庆文](https://pic1.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

13 人赞同了该文章



## 一、前言

本文开篇必须提到两个值得高兴的消息：

1. 有读者专门给我来信了，鼓励我坚持下去，有点受宠若惊，心里非常高兴，希望有更多读者，更多交流，有建议欢迎留言到我的微信公众号或者博客。
2. 新预览版： Godot 3.1 Alpha2 已经发布，也就是第二个预览版了，修复了一些问题，距离 Godot 3.1 正式版的发布又近了一步！着实激动人心。

之前的文章里我已经申明过：**我使用的是** **[Godot 3.1 预览版](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha2/)，如果要使用我所上传的[Github Demo 代码](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos)，那么务必到官网相应的版本哦！**下面附上最新预览版下载地址：

- Godot 3.1 Alpha2 各版本以及模板 Template 下载地址：[https://downloads.tuxfamily.org/godotengine/3.1/alpha2/](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha2/)
- Windows 操作系统 64 位版本文件，我这里已经单独列出来：[https://downloads.tuxfamily.org/godotengine/3.1/alpha2/Godot_v3.1-alpha2_win64.exe.zip](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha2/Godot_v3.1-alpha2_win64.exe.zip)
- Godot Engine 官方关于最新预览版的相关介绍：[https://godotengine.org/article/dev-snapshot-godot-3-1-alpha-2](https://link.zhihu.com/?target=https%3A//godotengine.org/article/dev-snapshot-godot-3-1-alpha-2)

工欲善其事必先利其器，好了，继续我们的 Godot 入门系列。依然基于上一篇文章，本篇我会给大家熟悉的“金币收集者骑士”小 *Demo* 划上一个句号，几个简单必要的任务是：添加常见的 UI 界面；然后再加一点料——游戏的音乐效果。再浏览之前，请务必参考上一篇文章：

[刘庆文：Godot3游戏引擎入门之八：添加可收集元素和子场景4 赞同 · 4 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/48411581)

> 主要内容： 创建 UI 界面以及添加一些音效
> 阅读时间： 8-10 分钟
> 永久链接：[http://liuqingwen.me/blog/2018/11/09/introduction-of-godot-3-part-9-add-audio-effects-and-ui-elements/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/11/09/introduction-of-godot-3-part-9-add-audio-effects-and-ui-elements/)
> 系列主页：[http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 给游戏添加 UI 控件
2. 创建独立的游戏主界面，使用按键切换游戏场景
3. 添加一些背景音乐和其他效果

## Godot中的分组

在添加 UI 控件显示**金币收集数量**之前，我们需要思考三个小问题，这三个问题解决好了界面就非常简单了，接下来我们一个一个解决。第一个问题就是：如何判断游戏场景中的金币已经被收集？

这个问题其实很好解决，在[上一篇文章](https://zhuanlan.zhihu.com/p/48411581)中我们已经在 *AnimationPlayer* 制作消失动画并结合代码实现的过程中已经解决了：使用 *Signal* 信号！金币在被采集的时刻，也就是玩家 *Player* 和金币 *Coin* （ *Area2D* ）发生碰撞的那一刻，节点会发出`body_entered` 的信号，我们通过连接这个信号做出处理并切换了金币的消失动画，同样的道理，我们可以利用这个信号在游戏主场景中加以利用，在信号订阅函数中进行计数处理，但与之前不同的是：

- 信号处理场景不同：一个在金币子场景，一个在 Game 游戏主场景
- 信号处理数量不同：子场景中只有一个 Area2D 节点，主场景有很多个金币实例
- 信号处理方式不同：子场景中手动连接信号，主场景中我们要避免手动连接信号

因为这几点不同，我们引出了第二个问题：既然金币数量不确定，我们要避免手动连接信号，那么如何在代码中连接信号呢？这个问题非常简单，一句代码解决：`coin.connect('body_entered', target, 'your_method')` ，代码种`connect` 方法第一个参数为信号名称，第二个为目标即订阅者，第三个为处理信号的函数。这和我们之前使用编辑器连接信号是一样的效果，同样的，我们可以使用`disconnect` 方法取消信号的连接。

两个问题都解决了，那么我们的模板代码大概是这样的：

```text
# 这里的self指当前节点
$Coin1.connect('body_entered', self, '_on_Coin_collected')
$Coin2.connect('body_entered', self, '_on_Coin_collected')
$Coin3.connect('body_entered', self, '_on_Coin_collected')
# ……

# 碰撞处理函数
func _on_Coin_collected(body):
    # 处理金币收集
    pass
```

明显地这里引出了第三个问题：那么多金币，如何简便地、一次性地获取场景中所有金币呢？解决这个问题的核心在于使用 Godot 中的另一个重要概念： *Group* 分组！考虑一下分组的应用场景：游戏场景中有很多金币，他们同属于某个**金币**分组，我们通过 GDScrip 代码的某个方法，获取了这个分组的所有金币信息，然后使用一个循环就可以轻松解决上面的重复代码问题了。这就是 *Group* 的一个最简单的应用场景。理论结束，实践起来非常简单：在编辑器中创建分组，然后添加到金币子场景的节点即可！

![img](https://pic3.zhimg.com/80/v2-11bf4053938260b3e9d01befab2cf916_720w.jpg)godot_9_create_group.png

如上图，我们创建了一个 `coin` 分组，之后我们并不需要在游戏主场景中对每一个**金币实例**进行分组的添加工作，只需在**金币子场景**中直接给根节点 *Coin* 添加 `coin` 分组就可以了。

## 控件和字体设置

接下来我们需要把金币收集数量显示到游戏场景中！也是第一次接触 Godot 中的 UI 控件吧，哈哈。在 Godot 中使用控件和节点没有任何区别。 Godot 中所有的控件都是继承于 *Control* 节点，我们只需要添加相应的 UI 节点就能在场景中显示，需要注意的是：控件的渲染和普通节点一样，后面的节点会覆盖前面节点的显示！在游戏中 UI 界面一般都会显示在主界面的最上层，那么我们添加控件的时候就需要把节点置为根节点*Game* 的最后一个子节点。但是，这样做有个缺陷：一旦有新节点添加到游戏场景中，默认位置为最后，这就难免还要去修改 UI 元素。对于游戏开发者来说，时间就是金钱，那有没有办法让 UI 层忽略其他节点，一直显示在最顶层，达到一劳永逸的效果呢？那就有请“金钱节约者” *CanvasLayer* 隆重登场！

*CanvasLayer* 节点是一个特殊节点，它能确保渲染在最顶层，这正是我们所需要的。我们只要把所有控件节点设置为 *CanvasLayer* 层的子节点即可。说做就做，在主场景中添加一个 *CanvasLayer* 子节点，改名为 UI ，然后往它里面添加其他子节点：首先添加一个 *HBoxContainer* 控件节点，如同其名，这是一个内容水平排列的盒子容器；在该节点内部添加一个显示金币图片的控件 *TextureRect* 节点，以及一个计数文本标签节点：*Label* 控件。控件节点的属性设置如下：

- TextureRect 节点设置 `texture` 材质属性为金币图片
- Label 节点更名为 Score ，修改 `text` 属性即文本内容为： `Score: 0`
- HBoxContainer 容器节点的位置调整，在子菜单栏中点击 Layout 选择 Top Wide 即可

![img](https://pic3.zhimg.com/80/v2-aedf9bcfe94f6ddc05f719094592ed6a_720w.jpg)godot_9_UI_layout.png

如上图，这里的 *Layout* 属性是所有**容器节点**具有的属性， *Top Wide* 即顶宽，**占据视窗顶部位置并拉伸宽度到最大**。不过，现在有一个问题就是：文本标签中 *Score* 中的文字太小了！作为程序员，第一反应肯定是去找*字体大小属性*设置即可，不过在 Godot 中控件的文字大小并不能直接设置，我们必须先提供**字体资源**然后在此基础上设置字体大小！

这个字体资源就是 **Custom Font 自定义字体**，一般为 `ttf` 格式，准备好字体文件，点击 *Label* （ *Score* ） 标签，在 *Custom Fonts* 的 *Font* 属性标签下，选择 *New DynamicFont* 创建一个新的动态字体，点击新建的动态字体进入**字体资源相关设置面板**，把 `ttf` 格式的字体文件拖拽到面板的 *Font Data* 属性下，最后在属性面板里设置字体的大小，字体的轮廓、颜色等就可以了，操作稍微复杂，适应一下就好了。 :grin:

![img](https://pic2.zhimg.com/80/v2-cedf857e032c04e867cbaec149053d79_720w.jpg)godot_9_font_resource.png

**注意：如上图，这里我把新建的字体资源保存成了单独的文件**，该资源文件命名为`font.tres` ，这些资源在后面可以**重复利用**，如果你不知道如何保存相关资源，可以翻一下我之前的文章。 :smiley:

## 添加代码

金币分组已设置好， UI 界面也准备完毕，现在可以添加代码实现我们“梦寐以求”地计数功能了，哈哈。接下来，通过场景获取所有属于 `coin` 分组中的金币，然后把分组中的每个金币逐个连接到碰撞信号处理函数，最后在连接好的方法中实现计数功能，理论在前面已详述，在 *Game* 根节点代码基础上添加代码如下，可以参考我给的注释：

```text
# 省略代码……

# 添加 UI 后的代码
onready var scoreLabel = $UI/HBoxContainer/Score
var score = 0 # 用于统计金币收集数量

func _ready():
    # 从场景数中获取所有属于coin分组的节点
    var coins = self.get_tree().get_nodes_in_group('coin')
    for *Coin* in coins:
        # 手动连接信号，用connect方法，第三个参数为信号处理函数名
       coin.connect('body_entered', self, '_on_Coin_collected')

# 碰撞处理函数
func _on_Coin_collected(body):
    score += 1
    updateScore()

# 更新UI界面
func updateScore():
    scoreLabel.text = 'Score: ' + str(score)

# 省略代码……
```

代码很简单，唯一值得注意的是 `body_entered` 信号处理函数需要传递一个参数。编写代码过程中如果遇到有任何问题，随时可以在 Godot 编辑器中按 F4 搜索查看相关说明。

## 一点点音效

运行我们的游戏，左上角，终于知道自己口袋里有多少 Money 了吧？！不过好像还是缺少点什么？嗯，缺少点声音——金币收集后的音效。和很多其他游戏引擎一样，在 Godot 中添加普通的音效非常简单，准备好我们需要的音乐素材，一个节点即可搞定：*AudioStreamPlayer* ，注意，你会发现 Godot 中有其他两个节点：*AudioStreamPlayer2D* 和 *AudioStreamPlayer3D* ，它们分别应用于 2D 世界和 3D 世界中的音特，比如声音传播立体感、传输的距离感等，不过这里我们不需要。

我们给游戏添加两个音效，一个是金币收集后消失的音效，一个是游戏的背景音乐。

**金币收集音效**：在金币子场景中再添加一个节点 *AudioStreamPlayer* 作为音乐流载体，音效是在 `disappear` 消失动画开始播放后才同时进行，所以我们需要把音效添加到相应的动画轨道上。首先打开动画面板，选择我们已经创建好的消失动画，然后添加一个音频轨道： *Audio Playback Track* ，在弹出的界面中选择刚才添加的*AudioStreamPlayer* 节点，然后把准备好的音乐资源文件直接拖拽到新建的音频轨道上即可！简单，方便，又不失强大。 :smile:

![img](https://pic3.zhimg.com/80/v2-40d6e02fe4ac23b5b8c5830ab57a8a6a_720w.jpg)godot_9_add_audiostream.png

**游戏背景音乐**：同样地，在游戏主场景中添加一个 *AudioStreamPlayer* 节点，然后设置节点的 `stream` 音频流属性，只需要把准备好的背景音乐直接拖拽过去即可！另外，可以适当调整一下音乐的音量，这里我把 `Volume Db` 音量的分贝设置为了 `-20` 降低了背景音乐的音量，比较合适。

最后，添加一行代码，让场景加载完后自动播放背景音乐：

```text
# 省略代码……
onready var audioPlayer = $AudioStreamPlayer

func _ready():
    # 场景加载完毕后开启背景音乐
    audioPlayer.play()
    # 省略代码……
```

好了，运行游戏，收集几个金币，喝上几口凉茶，放松一下心情吧！骚年！ :laughing:

## 创建主场景

嗯，还没完！我们已经掌握了几个最基本的 UI 控件，在此基础上再把游戏打造的稍微完美一点。是时候介绍一波自己强大的游戏了！哈哈。和大部分游戏一样，我们给自己的*Demo* 添加一个入口界面作为启动后的主界面，在这个界面的功能是突出显示游戏的名字，告诉玩家如何开始新的旅途，以及说明游戏体验是如何高大上，写明游戏的创作者有多牛逼……嗯，有点飘了，你继续，我来写。 :joy:

这个界面并不复杂，两行文字即可，也恰如其分地体现了我们游戏的简陋，嘿嘿。首先新建一个子场景，因为主要是 UI 元素，使用*Control*节点作为根节点，改名为*StartMenu* ，添加一个 *CenterContainer* 作为直接子节点，并在其下添加一个*VBoxContainer* 垂直容器，容器内添加两个 *Label* 标签子节点。这几个节点的名字很好地解释了其功能： *CenterContainer* 是一个能把内容居中显示的容器，*VBoxContainer* 为一个内容垂直分布容器。这里我设置 *CenterContainer* 的 *Layout*布局属性为 *Full Rect* 全屏显示，而两个文本标签都设置了 *Align* 对齐属性为*Center* 居中，并写上几个“高大上”的文字。

给文本标签修改字体，这里我使用了之前保存的字体资源： `font.tres` 。不过，当我想在第二个标签中把字体放得更大、颜色更鲜艳、更突出表现的时候，你会发现一处修改，所有应用了该字体资源的文本标签都变了！为了标新立异，是不是又要重新创建一个独立的资源文件呢？别急，很显然， Godot 早已考虑到了这点，我们只需要让资源**唯一化**即可轻松达到目的！在标签属性面板中，选中我们的字体资源，然后打开属性面板上的选项，选择 *Make Unique* 就可以轻松搞定啦！

![img](https://pic1.zhimg.com/80/v2-10697a20ef4e40e73f9146e1cc6e7614_720w.jpg)godot_9_reuse_font_resource.png

最后，给主场景也添加一个背景音乐，和之前的节点设置稍微有差别的是，这里我给*AudioStreamPlayer* 节点上勾选了 `AutoPlay` 属性，也就是自动播放而无需使用代码进行控制了。我们的游戏界面做完了，保存好，按下 F5 启动游戏运行，这时候游戏还是会自动进入*骑士收集金币*的界面，这不是我们想要的，我们需要从 *StartMenu* 场景开始，所以要对主场景进行修改，在 *Project -> Project Settings -> Application -> Run -> Main Scene* 中，选择创建好的主界面 `StartMenu.tscn`即可修改主界面为我们创建的菜单界面， OK ，一切准备就绪！

![img](https://pic1.zhimg.com/80/v2-7521df25b861d81eeef45193bf5de07c_720w.jpg)godot_9_set_main_scene.png

别忘了添加切换场景的代码，否则按 Enter 键或者空格键都不会有任何效果：

```text
extends Control

# 游戏场景资源路径
var gameScene = 'res://Game.tscn'

func _input(event):
    if event.is_action_released('ui_accept'):
        # 当按下空格或者回车时切换场景到Game
        self.get_tree().change_scene(gameScene)
```

大功告成：

![img](https://pic3.zhimg.com/v2-36ed7a1eb3672e54fe52701fbeab4a9a_b.jpg)

## 三、总结

总算结束了——这个“高大上”且“及其无聊”的“骑士满地找钱”游戏，哈哈。不知道大家看完后感觉怎样？不管如何，我们还是来总结一下本次学习到的一些 Godot 中的新鲜知识点吧：

1. 给游戏添加 UI 控件元素，使用 CanvasLayer 节点
2. 创建独立的游戏主界面，使用按键切换游戏场景
3. 添加背景音乐和其他声音效果及动画、代码控制
4. 其他小知识点：分组、代码中信号连接、字体资源等

最后的最后，我所要提醒的是， Godot 所支持的音频文件包括 *OGG* 和 *WAV* 格式，前者一般用于背景音乐，后者用于短音效，而不支持 *MP3* 格式的音频，另外我们的游戏也缺少很多很多普通游戏应有的一些机制，比如结束、暂停机制，没有怪物敌人、粒子特效，无关卡设计，不支持多人游戏等等，当然，这完全有待我们将来的开发啦！尽情期待吧！

本次代码已经上传到 Github ，还是那句话，**原创非常不易**，希望大家喜欢！ :smile:

# Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（上）

[![刘庆文](https://pic2.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

17 人赞同了该文章

## 一、前言

时间飞快，我有一段时间没有发表博客了，这段时间并不忙，一方面我自己也在不断学习，另一方面暂时不知写哪方面的内容了，感觉 Godot 中一些基础的部分我都或多或少谈到了，所以我打算使用我们学习过的知识来做一个小游戏吧。

这个游戏非常简单，但是对于完全“门外汉”的初学者来时还算有一定难度，不过别急，我会把我制作这个小游戏的一些思路以及常用的技巧娓娓道来，而且源代码我于上周就已经上传到 Github 啦： [https://github.com/spkingr/Godot-Demos](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos) ，另外这个游戏来源于一本书：

[《 Godot Engine Game Development Projects 》www.packtpub.com/game-development/godot-game-engine-projects](https://link.zhihu.com/?target=https%3A//www.packtpub.com/game-development/godot-game-engine-projects)

官网也有这个[Demo(Coin Dash)](https://link.zhihu.com/?target=https%3A//github.com/PacktPublishing/Godot-Game-Engine-Projects) 以及其他示例的代码，我的思路和代码和官方有点不同，也实现了一些其他功能比如游戏暂停、金币数量显示等，强烈建议大家去围观。 :smiley:

![img](https://pic2.zhimg.com/v2-afd534cc21d0ac8c444bd7f7f455a489_b.jpg)

本文分上下两篇，第一篇，也就是在进入“金币”小游戏的开发制作讲解之前，我先把之前文章里没有遇到过的一些非常重要的节点介绍一下，还有一个提醒：最好的学习方法应该是先尝试一遍或者边思考边把代码浏览一下，然后再来看我的文章，这样效果会比较好。嗯，废话不多说，我们开始吧！

> 主要内容：认识一些新的节点和代码学习阅读时间： 10 分钟永久链接： [http://liuqingwen.me/blog/2018/11/30/introduction-of-godot-3-part-10-introduce-some-node-types-and-make-a-new-game-part-1/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/11/30/introduction-of-godot-3-part-10-introduce-some-node-types-and-make-a-new-game-part-1/)系列主页： [http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 学习使用一些新的 Godot 节点
2. 最基本的游戏开发规则
3. 编写代码的规范

## Godot 中常用节点

**1. Timer 节点**

看名字就知道这是一个“计时器”。在 Godot 中**一切皆节点**，所以看到这种*纯功能性*的节点不要觉得奇怪，同时，我们完全可以不使用节点，直接使用代码 `Timer.new()` 动态创建一个计时器也是没任何问题的；甚至我们完全可以通过设置变量，利用`_process(delta)` 方法来计算时间，不过显然没有 *Timer* 节点来得方便简洁！

![img](https://pic2.zhimg.com/80/v2-b4074e9aea28e971eeea5e36c0a24a8d_1440w.jpg)godot_10_timer_node.png

[godot_10_timer_node.png](https://link.zhihu.com/?target=http%3A//godot_10_timer_node.png/)

Timer 时间计时器节点的属性非常简单，根据需求可以设置其等待时间、重复计时以及是否自动开始，这些属性我们也可以在 GDScript 脚本中使用代码修改：

- `wait_time` ：等待时间，即计时时长，结束触发 `timeout` 信号
- `one_shot` ：是否是一次性，如果是，只会触发一次 `timeout` 信号
- `autostart` ：自动开始，载入场景后计时，也可以使用 `start` 方法手动开启

游戏中计时功能使用非常频繁，不过，有部分计时场合我们还可以使用 `yield` 关键字代替，这样会省去节点的创建和信号的连接等繁琐、重复代码，这是分使用场合的，后面我会详述。 :smile:

**2. Tween 节点**

在游戏开发过程中，我们一般使用 *AnimationPlayer* 节点来实现移动、缩放、颜色渐变等动画效果，但实际上，在有些场景中我们可能会直接使用 *AnimatedSprite* 节点，再结合一系列图片来实现动画特效，这个时候由于图片的限制（比如我们只做了金币的闪耀图片，并没有做金币的消失图片），我们并不能添加实现其他普通动画，那是不是没有其他办法呢？——办法当然有，这就需要 *Tween* 节点的隆重登场了！

![img](https://pic1.zhimg.com/80/v2-4b8b18b4e0fb732bd3a952a725ce158c_720w.jpg)godot_10_tween_node.png

Tween 即*渐进/过渡*的意思，从一种状态在一定时间内变化到另一种状态，从而产生一种视觉动画。渐变节点使用非常简单方便，可以对一个物体的任意属性进行动画控制，当然，也可以同时处理多个动画对象。其主要方法有以下几个：

- `repeat` ：是否重复
- `start()` ：开始渐变，结束后触发 `tween_completed` 信号
- `interpolate_property()` ：设置进行动画的节点属性以及时长等，需要传递属性名称、开始结束值、时长等参数

这里最重要的方法是 `interpolate_property()` ，可以在 Godot 编辑器中按 F4搜索 *Tween* 类进行查看。当然，和 *Timer* 节点一样，我们完全可以在代码中动态创建*Tween* 对象。

**3. Path2D 节点**

*Path2D* 是一个路径节点，由很多位置点组成，这个路径可以是曲线，也可以是直线。实际上 *Path2D* 一般是与 PathFollow2D 配合使用，关于 *Path2D* 的使用，我推荐去看看官方的一个例子： [Your first game](https://link.zhihu.com/?target=https%3A//docs.godotengine.org/en/latest/getting_started/step_by_step/your_first_game.html) 。

![img](https://pic4.zhimg.com/v2-fbc54e42a0cfc111cf510f1e6f3ad947_b.jpg)

在我要讲解的这个小 Demo 中，我使用 *Path2D* 路径节点绘制了一些点来保存需要用到的位置，后续我会详述。 :smiley:

![img](https://pic4.zhimg.com/80/v2-cddcc7eb63806ae807a5cffde7478a3f_720w.jpg)godot_10_path2d_node.png

## GDScript 几个重要关键字

*1. export(PackedScene)/export(AudioStream)*

在之前的文章中我们使用过 `export(int) var speed = 10` 来定义一个可以在编辑器中修改设置的整数值，以表示速度，同样地，我们可以使用 `export` 关键字来定义可以在编辑器中编辑的其他类型变量，比如：子场景、音频流等。

`export(AudioStream)` 用于定义一个*音频流*变量， `export(PackedScene)` 用于定义一个*子场景*变量，想象一下，游戏中我们制作了 3 种不同颜色的金币，每个关卡使用的金币可能不一样，这里我们就可以在关卡中定义一个 `PackedScene` 变量，然后直接在编辑器中选择对应的金币进行设置就可以了，非常方便。有点抽象，不过在后面的游戏代码中我们会应用到。

*2. preload('res://resource.tscn')*

`preload` 方法可以在代码中动态加载场景、文字、图片、音频等资源，比如我们可以预加载制作好的金币子场景，然后在代码中实例化，生成多个金币节点并添加到舞台中，实现动态添加金币的效果。 `preload` 是一个常用方法，不过在这个游戏中我并没有使用到，暂时提一下，以后讲 [Singleton](https://link.zhihu.com/?target=http%3A//docs.godotengine.org/en/3.0/getting_started/step_by_step/singletons_autoload.html) 单例再详述吧。

*3. ProjectSettings.get('display/window/size/width')*

在游戏创建的时候，我们都会对项目相关属性进行设置，比如游戏屏幕显示尺寸大小等，那么如何在代码中动态获取这些参数值呢？我们可以直接使用 `ProjectSettings` 这个单例，通过传入属性的路径，比如窗口大小的高度： `display/window/size/height`即可获取相对应的配置值，这样能避免*硬编码*，即使修改了配置游戏依然能正常运行！

*4. rand_range/randomize/randi*

很多游戏中都会大量使用**随机**值，比如金币数量随机、金币品类随机、出现时机随机等等，在 GDScript 脚本中使用随机同样非常简单直接，一个方法 `randi()` 即可生成一个随机整数，不过这个整数的范围很大，需要生成范围限制的随机数则可以用`rand_range()` 方法，接收两个参数，一个最小值，一个最大值。

除了这两个方法，还有一个 `randomize()` 方法，这个方法有什么用呢？如果你在游戏中使用随机数，你会发现每次运行游戏，这个随机数都是相同的，这是因为生成随机数需要一个 `seed` 也就是名为**种子**的整数，因为种子并没有随机，所以根据这颗种子生成的随机数自然也就不会变化了，如何做到真正的随机呢？——在使用随机方法前，调用一下`randomize()` 方法就可以啦！

*5. get_tree().paused*

我在游戏中添加了**暂停**的功能，相信大部分游戏都有这个功能吧。在 Godot 中暂停功能非常容易实现！直接调用 `get_tree().paused = true` 这一行代码就可以了，是不是感觉非常轻松直接？哈哈，不过记住：一旦运行这行代码后，我们的游戏会**完全处于暂停状态**，也就是说不论游戏本身、还有输入、甚至弹出的 UI 界面等都一律等闲视之——后果就是你不能继续游戏了！

当然，解决这个问题是非常简单的，我们只需要把*那些不被默认暂停的元素（暂停状态下依然可用）*的 *Pause Mode* 暂停模式设置由 `inherit` 属性改成 `process` 就可以了：

![img](https://pic3.zhimg.com/80/v2-1330b4d0dbd04ecef7e9c852d209d64a_720w.jpg)godot_10_pause_mode.png

*6. yield()*

这可以算是 GDScript 脚本的一个高级功能，它和 Python 中的 `yield` 关键字如出一辙，如果你熟悉*协程*的概念，像 Unity C# 中的 `StartCoroutine()` 方法， Kotlin 中的 `Coroutine` 协程， Dart/JavaScript 语言中的 `await/async` 关键字，那么 `yield` 的工作原理是很好理解的。

> 对于新手来说，我觉得可以把协程简单地理解为：程序运行到该位置（ yield ），暂停挂起在当前位置，继续执行其他代码，当时机到来，回到刚才挂起的位置继续执行。

嗯，听起来有点玄乎，不过在代码中使用起来非常简洁，参考运行下面的代码吧：

```text
print('开始运行程序……')
yield(get_tree().create_time(1.0), 'timeout') # 挂起 1 秒钟
print('1秒钟后输出：结束运行。')
```

## 游戏开发的几个小 Tips

几个实用的小技巧或者说开发规则，也是我自己在开发实践中、他人的书籍里、一些博客文章中学到的，总结的不多，不过对于初学者来说还是比较重要的，可以先按部就班，之后再发展处自己的风格思路吧！ :grin:

**1. 文件夹的管理**

在我之前的文章里，对于小项目我都没有做特殊的文件管理，但是当游戏项目越来越大的时候，我们需要引起足够的重视，因为这会影响开发速度、以及团队合作的效率。其实，你完全可以按照自己的风格去管理资源文件，但是更推荐官方的一些做法和建议：

[Project organizationdocs.godotengine.org/en/3.0/getting_started/workflow/project_setup/project_organization.html](https://link.zhihu.com/?target=https%3A//docs.godotengine.org/en/3.0/getting_started/workflow/project_setup/project_organization.html)

```text
/project.godot
/docs/.gdignore
/docs/learning.html
/models/town/house/house.dae
/models/town/house/window.png
/models/town/house/door.png
/characters/player/cubio.dae
/characters/player/cubio.png
/characters/enemies/goblin/goblin.dae
/characters/enemies/goblin/goblin.png
/characters/npcs/suzanne/suzanne.dae
/characters/npcs/suzanne/suzanne.png
/levels/riverdale/riverdale.scn
```

这里我简单地比较了 Unity 和 Godot 中文件管理的风格样式，我个人更倾向于 Godot 的文件组织方式，因为等会我还会讨论一条重要的开发原则：**尽量保持每个子场景的独立性**！

![img](https://pic4.zhimg.com/80/v2-70861e52f80c92eeacc5ce9cbdcee9ef_720w.jpg)file_orgnization_unity_vs_godot.png

**2. 保持场景独立**

嗯，我认为这是 Godot 中开发游戏最重要的一条原则了！它能明显地提升开发效率，提高团队合作，更利于 Debug 调试。因为 Godot 中一切基于场景，场景中可以包含多个子场景，子场景依然可以由多个其他子场景组成，而且**每个子场景是可以单独运行的！**打开子场景，按 F6 来单独运行、测试，及早发现问题，提高程序的健壮性。

如何保持场景独立？这就需要我们去仔细思考了，具有独立功能的部分我们都可以抽离出来作为一个单独的子场景，通用、具有类似功能的节点也可以抽离出来以继承关系实现，需要说明的是：**独立并不意味着不与其他场景发生任何关系了**，独立只是让它能单独运行，能单独测试一部分功能，这是很重要的。

**3. 代码编写规范**

代码构成了游戏的灵魂，代码编写不规范带来的直接后果就是：

- 自己看不懂，遇到 BUG 后越改越乱
- 团队里其他开发者看不懂，很难或者无法 DEBUG
- 不利于后续功能的开发、重构等

和文件组织管理方式一样，其实代码编写规范也会因人而异，在 Godot 中官方所推荐的方式如下：

```text
# 枚举、常量等变量命名
enum State{INIT, IDLE, PLAYING, DEAD}
const CONST_GRAVITY = 98

# 普通变量、私有变量命名
var player_sprite = 1
var _walk_speed = 2

# 私有方法命名
func _private_method():
    get_tree().paused = true
    pass

# 公有方法命名
func public_method():
    _private_method()
    pass
```

注意，在 GDScript 中是没有 `private/public/protected` 等关键字来规范访问限制的，类似 Python ，这也正是我们需要保持一定的编码规范的原因之一。不过，你会发现我的命名方式会有所不同！我比较习惯 Java/C#/Dart 等语言的命名规则，采用*驼峰式*，同时利用 `_` 下横线来标记私有变量或者方法，而且调用*内部方法*的时候我都会*显式*使用 `self` 关键字：

```text
# 枚举、常量等变量命名
enum State{INIT, IDLE, PLAYING, DEAD}
const CONST_GRAVITY = 98

var playerSprite = 1 # 公有变量
var _walkSpeed = 2 # 私有变量

# 私有方法命名
func _privateMethod():
    self.get_tree().paused = true
    pass

# 公有方法命名
func publicMethod():
    _private_method()
    pass
```

至于选哪种，我觉得只要保持规范，符合个人或者团队共识就好啦！ :smiley:

## 三、总结

本篇文章算是一个经验小总结吧，也是为了更好地解释我们后面要出场的游戏项目，林林总总地列举了一些不成文的条条列列，不知道大家看后的感受是怎样的呢？

嗯，有两周没有写文章了，因为最近有其他的事情和同学在忙乎，不过我一定会坚持下去的，还是那句话，**原创非常不易**，希望大家喜欢！ :smile:



# Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（中）

[![刘庆文](https://pic1.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

4 人赞同了该文章

## 一、前言

上篇文章：

[刘庆文：Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（上）17 赞同 · 0 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/51282054)

我们一起学习探讨了几个常用的新节点，也顺便了解一下 GDScript 脚本中几个重要关键字的用法，最后总结了我个人认为比较实用的几个所谓“最佳实践”，写了这么多的目的就是为了本篇和下一篇服务的：我们使用 [Godot 3.1 Alpha2](https://link.zhihu.com/?target=https%3A//downloads.tuxfamily.org/godotengine/3.1/alpha2/) 版本制作一个小游戏。

这个游戏非常简单，网上也有不少类似的案例，本来打算只需要上下两篇文章即可，后面发现加上代码后整篇文章显得“篇幅过长”，如果通过删减一些代码来缩短篇幅的话，对新手又很不友好，所以我再加一篇，分为“上-中-下”三篇吧。

温馨提示：中篇以及下篇内容中的代码会比较多，如果对这个游戏感兴趣，而且已经入门的话，我推荐直接到我的 [Github 仓库](https://link.zhihu.com/?target=https%3A//github.com/spkingr/Godot-Demos)下载源码运行查看即可，或者遇到了问题再来翻阅此文更合适。 :smile:

> 主要内容：分析并制作一个完整的小游戏（中篇）
> 阅读时间： 12 分钟
> 永久链接： [http://liuqingwen.me/blog/2018/12/05/introduction-of-godot-3-part-10-introduce-some-node-types-and-make-a-new-game-part-2/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/12/05/introduction-of-godot-3-part-10-introduce-some-node-types-and-make-a-new-game-part-2/)
> 系列主页： [http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 了解学习游戏中的几个主要场景的制作
2. 编写代码实现游戏中相关功能的逻辑
3. 完整游戏项目的一个开发流程

## 主要的场景

这是一个简单的“金币收集小游戏”，游戏设计的主要思路和玩法大致如下：

- 玩家可以在自由的世界里随处奔跑，遇到心爱的金币可以尽收囊中
- 玩家要避免被仙人掌刺伤，这也是游戏的唯一实体障碍物
- 每个关卡有超时时间设计，超时游戏结束，规定时间内收集完金币可进入下一关
- 每关随机冒出一个特殊“能量币”，玩家收集能量能够延长超时时间

嗯，时间紧迫，上车，赶紧出发！

## **1. Player 玩家子场景**

玩家子场景是这个项目的最核心游戏元素，可以说是小游戏的灵魂所在。玩家子场景的制作非常简单：以碰撞体 *Area2D* 作为根节点，添加一个 *Sprite* 图片精灵、一个*CollisionShape2D* 绘制碰撞区域、 *AnimationPlayer* 节点制作动画以及一个*AudioStreamPlayer* 音频流播放节点。如果对这些节点的使用不熟悉，可以参考我之前的文章。

![img](https://pic1.zhimg.com/80/v2-446010b778cdf8b1e00ee822ac5e2058_720w.jpg)godot_10_player_scene

另外，因为我把玩家的动画图片制作成了一个 SpriteSheet 精灵图集，所以制作动画的时候需要注意图片的显示区域，玩家有三个动画状态，都比较简单，参考如下：

![img](https://pic3.zhimg.com/80/v2-bfaa79a2edda7ac4b805b4af7803620e_720w.jpg)godot_10_player_animation

## **2. Coin/Cactus/Power 金币/障碍物/能量子场景**

我把这三个小场景放到一起讨论，原因是它们的结构非常简单且很相似，都是为游戏中的“玩家”服务。三个子场景的制作一目了然，功能单一，相互独立，这也符合我们的最佳实践原则之*尽量保持场景的独立性*。另外，在对游戏资源的管理中，我把这三个场景以及场景的相关资源（图片）放在了 *Items* 一个文件夹下。

![img](https://pic2.zhimg.com/80/v2-53d335dbd9ee7bfb1563ee4176ae83c9_720w.jpg)godot_10_items_scene

需要注意的是：能量币场景中的 *LifeTimer* 时间节点表示金币在规定时间内会自动消失，而能量币的出现时间并不由自己控制，这里不要混淆了，后面在代码中会有介绍。

## **3. UI 界面元素**

控件子场景主要用于界面显示，主要有：金币数量、剩余时间、开始按钮、文字信息显示等。这里我使用了 *MarginContainer* 容器配合 *HBoxContainer/VBoxContainer* 来对界面元素进行排版。提醒新手朋友们：设置 *MarginContainer* 的边距需要在 *Custom Constants* 属性下进行设置。

![img](https://pic1.zhimg.com/80/v2-317b1f17d140dbc0278d9fbabf8e038c_720w.jpg)godot_10_ui_scene

另外 UI 子场景也用于接收玩家的键盘输入，控制游戏的一些基本逻辑：开始、暂停、重试等，这些我们都会在代码中具体实现。

## **4. 游戏主场景**

这是游戏中最重要的场景了，也是包含并协调多个子场景的根场景。游戏的主场景中可以手动添加其他的节点或者子场景，也可以通过代码添加任意多个子场景，比如金币。同时，主场景负责并处理每个子场景之间通信链接，作为一个*总指挥*让每个子场景各司其职，及时得到并处理各自的相关任务。

![img](https://pic2.zhimg.com/80/v2-7dfa8469149a939d860608b1f105e0c1_720w.jpg)godot_10_game_scene

值得注意的是：我把障碍物场景（ *Cactus* ）作为子节点放在了 *Path2D* 路径节点之下，也就是图中的蓝色路径。场景中的 *CoinContainer* 为一个空节点，作为动态生成的金币节点的容器。

## 逻辑与代码

在 Godot 中每一个节点都能添加代码，而且最多只能关联一个脚本，一般子场景的功能相对单一，我们优先考虑给子场景的根节点添加一个脚本，而其他节点可以视需求添加，需要说明的是：**子场景中需要暴露出来的供其它场景调用的公开方法最好写在根节点的脚本代码中**。

另外，实现游戏的相关功能以及逻辑代码并不是只有唯一的一种方式，你完全可以根据自己的需求、设计原则、游戏规则等来进行代码编写。 :smiley:

> 说明：这个小游戏的灵感和图片资源都来源于[《 Godot Engine Game Development Projects 》](https://link.zhihu.com/?target=https%3A//www.packtpub.com/game-development/godot-game-engine-projects)这本书，我参考了它的代码，但是我的设计方式与之稍有不同，比如在处理玩家和金币碰撞的逻辑上有两种方式，是在 *Player* 玩家场景中检测碰撞并调用*Coin* 的方法，还是在 *Coin* 金币场景中检测碰撞并调用 *Player* 的方法，此书的作者采用了前者，而我选择了后者。我的观点是：游戏元素为玩家服务，玩家不需要关心游戏世界里有哪些元素。当然，运行结果完全相同。

接下面我把游戏中的主要代码贴出来供大家参考阅读，如果遇到不懂的地方可以随时翻阅我之前的文章，或者直接在 Godot 编辑器中按 F4 搜索查看相关的 API 说明，相信配合我在脚本中的注释，看懂代码的具体逻辑没什么问题。 :grin:

## *1. Player.gd*

```text
extends Area2D

# signal group
signal coin_collected(count) # 金币收集信号
signal power_collected(buffer) # 能量币收集信号
signal game_over() # 游戏结束信号

# export
export(int) var moveSpeed = 320
export(AudioStream) var coinSound = null
export(AudioStream) var hurtSound = null
export(AudioStream) var powerSound = null

# onready
onready var _animationPlayer = $AnimationPlayer
onready var _audioPlayer = $AudioStreamPlayer
onready var _sprite = $Sprite

# enum, constant

# variable
var isControllable = true setget _setIsControllable # 是否允许玩家被控制
var _coins = 0 # 当前关卡所收集金币的数量
var _boundary = {minX = 0, minY = 0, maxX = 0, maxY = 0} # 移动范围

# functions
func _ready():
    var scale = _sprite.scale
    var rect = _sprite.get_rect()

    # 设置玩家能移动的上下左右最大范围
    _boundary.minX = - rect.position.x * scale.x
    _boundary.minY = - rect.position.y * scale.y
    _boundary.maxX = ProjectSettings.get('display/window/size/width') - (rect.position.x + rect.size.x) * scale.x
    _boundary.maxY = ProjectSettings.get('display/window/size/height') - (rect.position.y + rect.size.y) * scale.y

func _process(delta):
    # 根据玩家键盘输入设置玩家的移动方向和速度
    var hDir = int(Input.is_action_pressed('right')) - int(Input.is_action_pressed('left'))
    var vDir = int(Input.is_action_pressed('down')) - int(Input.is_action_pressed('up'))
    var velocity = Vector2(hDir, vDir).normalized()
    self.position += velocity * moveSpeed * delta
    self.position.x = clamp(self.position.x, _boundary.minX, _boundary.maxX)
    self.position.y = clamp(self.position.y, _boundary.minY, _boundary.maxY)

    if hDir != 0:
        _sprite.flip_h = hDir < 0
    if hDir != 0 || vDir != 0:
        _animationPlayer.current_animation = 'run'
    else:
        _animationPlayer.current_animation = 'idle'

# isControllable属性的set方法
func _setIsControllable(value):
    if isControllable != value:
        isControllable = value
        self.set_process(isControllable)
        _animationPlayer.current_animation = 'idle' if ! isControllable else _animationPlayer.current_animation

# 重新开始的方法，传递一个玩家初始位置
func restart(pos):
    _coins = 0
    self.position = pos

# 收集金币方法，传递收集金币数量
func collectCoin(num = 1):
    _coins += num
    _audioPlayer.stream = coinSound
    _audioPlayer.play()
    self.emit_signal('coin_collected', _coins)

# 收集到能量调用的方法
func collectPower(buffer):
    _audioPlayer.stream = powerSound
    _audioPlayer.play()
    self.emit_signal('power_collected', buffer)

# 玩家受到伤害时用方法
func hurt():
    _animationPlayer.current_animation = 'hurt'
    _audioPlayer.stream = hurtSound
    _audioPlayer.play()
    self.set_process(false)
    self.emit_signal('game_over')
```

玩家场景的代码部分相对较多，在此我特意标明了我的源码编写习惯，一般保持良好的代码风格是有利于游戏的调试和功能的扩展的，代码中我习惯的编码顺序是：

1. *signal/group* 信号、分组写代码文件最前
2. *export* 接着是显示在编辑器中可编辑的相关变量
3. *onready* 主要表示一些对场景中的节点的引用
4. *enum/constant* 枚举、常亮定义部分（无实际代码）
5. *variable* 普通变量定义部分（公开的、私有的）
6. *functions* 最后是方法函数定义部分（公开的、私有的）

关于函数部分也要注意一些小细节， GDScript 脚本中有公开方法和私有方法，这些方法的位置可以随意，只要自己看着舒服就可以啦。其中几个关键地方我简单解释下：

- `self.set_process(false)` 这个方法能暂停或开启`_process(delta)` 方法的运行，部分类似暂停游戏
- `self.emit_signal('power_collected', buffer)` 发射信号的方法，已经讨论过了，不过这里额外添加了一个参数
- `_audioPlayer.stream = xxx` 玩家场景中只使用一个音频节点，通过设置不同的 `stream` 音频流可以播放不同的音效

其他部分请参考注释吧。

## *2. Coin.gd*

```text
extends Area2D

# 玩家名字，根据玩家名字判断金币否被收集
export var playerName = 'Player'
# 障碍物名字，如果金币与障碍物重叠则重新生成
export var obstacleName = 'Cactus'

onready var _collisionShape = $CollisionShape2D

func _on_Coin_area_entered(area):
    # 判断碰撞体是否为玩家
    if area.name == playerName && area.has_method('collectCoin'):
        _collisionShape.disabled = true
        area.collectCoin()
        self.queue_free()
    # 如果是障碍物则删除该金币
    elif area.name == obstacleName:
        self.queue_free()
```

金币节点非常简单，代码也很简洁，主要功能是：玩家收集后自动消失，同时调用玩家的收集函数 `collectCoin()` 。为防止调用出错，我在代码中对玩家是否有该方法做了判断。

## *3. Cactus.gd*

```text
extends Area2D

export var playerName = 'Player'

func _on_Cactus_area_entered(area):
    # 与玩家相撞，调用玩家的hurt方法
    if area.name == playerName && area.has_method('hurt'):
        area.hurt()
```

这是最简单的子场景了！游戏规则就是：玩家碰到障碍物（仙人掌）后，玩家收到伤害，游戏结束。逻辑代码可以参考 *Player* 场景的 `hurt()` 方法。

## *4. Power.gd*

```text
extends Area2D

export var playerName = 'Player'
export var power = 2 # 能量蕴藏的时间参数

onready var _collisionShape = $CollisionShape2D
onready var _sprite = $Sprite
onready var _timer = $LifeTimer
onready var _tween = $DisappearTween

# 使用Tween节点实现放大到消失的动画
func _startTween():
    _tween.interpolate_property(_sprite, 'modulate', Color(1.0, 1.0, 1.0, 1.0), Color(1.0, 1.0, 1.0, 0.0), 0.25, Tween.TRANS_CUBIC, Tween.EASE_IN_OUT)
    _tween.interpolate_property(_sprite, 'scale', _sprite.scale, _sprite.scale * 4, 0.25, Tween.TRANS_CUBIC, Tween.EASE_IN_OUT)
    _tween.start()

func _on_Power_area_entered(area):
    # 玩家收集到能量
    if area.name == playerName && area.has_method('collectPower'):
        _collisionShape.disabled = true
        area.collectPower(power)
        _timer.stop()
        _startTween()

# 一定时间后能量币消失
func _on_LiftTimer_timeout():
    self.queue_free()

# 动画结束后消失
func _on_Tween_tween_completed(object, key):
    self.queue_free()
```

和金币、障碍物一样，也是一个很简单的子场景，不过我们使用了 *Tween* 节点，利用代码实现能量币的消失动画。关于 *Tween* 节点可以参考[上一篇文章](https://zhuanlan.zhihu.com/p/51282054)，对于方法中每个参数的定义可以直接查阅官方 API 文档。

## 其他部分

其他部分的代码以及总结部分见下篇！**未完待续……**



# Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（下）

[![刘庆文](https://pic2.zhimg.com/69b29bc3a41e36c548988c2e2d5022f9_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/liu-qing-wen-36)

[刘庆文](https://www.zhihu.com/people/liu-qing-wen-36)

关注他

7 人赞同了该文章

## 一、前言

继续前面的两篇文章，《Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏》一共分为三小篇，链接如下：

[刘庆文：Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（上）17 赞同 · 0 评论文章![img](https://pic3.zhimg.com/v2-112ce27cc51a475d49fc3e6b22d5008a_180x120.jpg)](https://zhuanlan.zhihu.com/p/51282054)

[刘庆文：Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（中）4 赞同 · 0 评论文章![img](https://pic3.zhimg.com/v2-b293558884dcd33b387bc36b2b3fefc6_180x120.jpg)](https://zhuanlan.zhihu.com/p/51839824)

[刘庆文：Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（下）7 赞同 · 1 评论文章![img](https://pic3.zhimg.com/v2-b293558884dcd33b387bc36b2b3fefc6_180x120.jpg)](https://zhuanlan.zhihu.com/p/51840916)

> 主要内容：分析并制作一个完整的小游戏（下篇）
> 阅读时间： 6 分钟
> 永久链接： [http://liuqingwen.me/blog/2018/12/06/introduction-of-godot-3-part-10-introduce-some-node-types-and-make-a-new-game-part-3/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/2018/12/06/introduction-of-godot-3-part-10-introduce-some-node-types-and-make-a-new-game-part-3/)
> 系列主页： [http://liuqingwen.me/blog/tags/Godot/](https://link.zhihu.com/?target=http%3A//liuqingwen.me/blog/tags/Godot/)

## 二、正文

## 本篇目标

1. 了解学习游戏中的几个主要场景的制作
2. 编写实现游戏中相关逻辑的代码
3. 分析整个项目的一个开发流程

## 主要的场景

请参考上一篇：[Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（中）](https://zhuanlan.zhihu.com/p/51839824)。

## 代码与逻辑

部分代码见上篇文章：[Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（中）](https://zhuanlan.zhihu.com/p/51839824)。

相关的细节解释参考：[Godot3游戏引擎入门之十：介绍一些常用的节点并开发一个小游戏（上）](https://zhuanlan.zhihu.com/p/51282054)。

接下来是 UI 控件场景和 Main 游戏主场景的脚本代码，相对来说比较长，但是不难理解，相关重要的地方我已经做了注释，相信您能一目十行。 :grin:

## *5. UI.gd*

```text
extends Control

# 开始游戏的信号
signal start_game()

onready var _labelScore = $MarginContainer/HBoxContainer/LabelScore
onready var _labelTime = $MarginContainer/HBoxContainer/LabelTime
onready var _labelMessage = $VBoxContainer/LabelMessage
onready var _labelReady = $VBoxContainer/LabelReady
onready var _buttonStart = $MarginContainer2/ButtonStart

# 当前游戏是否被暂停，初始为“是”
var _isPaused = true

# 监听用户的输入
func _input(event):
    if event.is_action_pressed('start'):
        # 这个if条件语句只会在游戏开始时运行一次！
        if self.get_tree().paused != _isPaused:
            self.emit_signal('start_game')

        _isPaused = ! _isPaused
        self.get_tree().paused = _isPaused
        if _isPaused:
            _labelMessage.visible = true
            _labelMessage.text = 'Paused'
        else:
            _labelMessage.visible = false
            _buttonStart.visible = false

# 开始游戏按钮被按下
func _on_ButtonStart_pressed():
    _isPaused = false
    _labelMessage.visible = false
    _buttonStart.visible = false
    self.emit_signal('start_game')

# 显示Ready和目标金币数文本
func displayReady(target = 0, display = false):
    _labelReady.text = '%d, Ready!' % target
    _labelReady.visible = display

# 游戏结束显示的信息
func showGameOver():
    _isPaused = true
    _labelMessage.text = 'Game Over'
    _labelMessage.visible = true
    _buttonStart.text = 'Restart'
    _buttonStart.visible = true

# 显示分数（金币个数）
func showScore(score):
    _labelScore.text = str(score)

# 显示时间（剩余时间）
func showTime(time):
    _labelTime.text = str(time)
```

UI 子场景代码稍复杂，不仅要显示一些文字信息，比如当前时间、收集到的金币数等，还负责接收响应玩家的键盘输入，处理开始、暂停以及游戏重试等。当然，逻辑并不复杂。

唯一要注意的地方是 `if self.get_tree().paused != _isPaused:` 这个判断语句，我在代码中已经作了相关说明，它的判断结果只有在游戏开始运行的第一次时为`true` ，其他任何时间都为 `false` （因为 `_isPaused` 的初始值的原因），也就是表示在开始游戏的时候玩家按了 `start` 按键（我在 *Input Map* 中设置 `start`输入为空格和回车），然后发射游戏开始的信号。当然，你完全可以再定义一个变量来实现游戏的开始和暂停等。

## *6. Game.gd*

```text
extends Node2D

export(PackedScene) var coinScene = null
export(PackedScene) var powerScene = null
export(float) var minPlayerDist = 80
export(float) var minObstacleDist = 120

onready var _player = $Player
onready var _startPosition = _player.position
onready var _ui = $HUD/UI
onready var _pointsCurve = $CactusPoints.curve
onready var _cactus = $CactusPoints/Cactus
onready var _coinContainer = $CoinContainer
onready var _countTimer = $CountTimer
onready var _powerTimer = $PowerTimer
onready var _gameOverAudioPlayer = $GameOverAudio
onready var _levelAudioPlayer = $LevelUpAuido

var _level = 0 # 当前关卡
var _timeLeft = 0 # 剩余时间
var _totalCoins = 0 # 金币总数
var _collectedCoins = 0 # 收集金币数

func _ready():
    randomize() # 保证每次游戏都随机
    _player.isControllable = false

# 游戏结束初始化某些变量
func _gameOver():
    _level = 0
    _countTimer.stop()
    _ui.showGameOver()
    for coin in _coinContainer.get_children():
        coin.queue_free()

# 重新开始游戏调用方法
func _restartGame():
    _player.isControllable = false
    _totalCoins = _calculateTotal(_level)
    _timeLeft = _calculateDuration(_level)
    _collectedCoins = 0
    _ui.showScore(_collectedCoins)
    _ui.showTime(_timeLeft)
    _spawnObstacles()
    _spawnCoins()
    _player.restart(_startPosition)

    _ui.displayReady(_totalCoins, true)
    # 关键代码，如果不明白可以参考后面的解释
    yield(self.get_tree().create_timer(1.5, false), "timeout")
    _ui.displayReady()
    _player.isControllable = true
    _countTimer.start()
    _spawnPowerup()

# 进入下一关卡
func _nextLevel():
    _level += 1
    _restartGame()

# 玩家收集金币发出的信号处理
func _on_Player_coin_collected(count):
    _ui.showScore(count)
    if count >= _totalCoins:
        _countTimer.stop()
        _levelAudioPlayer.play()
        _nextLevel()

# 玩家受到伤害，游戏结束信号处理
func _on_Player_game_over():
    _gameOver()

# 玩家收集到能量币发出的信号处理
func _on_Player_power_collected(buffer):
    _timeLeft += buffer
    _ui.showTime(_timeLeft)

# 游戏时间超时，游戏结束
func _on_Timer_timeout():
    _timeLeft -= 1
    _ui.showTime(_timeLeft)
    if _timeLeft <= 0:
        _player.isControllable = false
        _gameOverAudioPlayer.play()
        _gameOver()

# 能量币定时生产
func _on_PowerTimer_timeout():
    var power = powerScene.instance()
    var pos = _makeRandomPosition()
    power.position = pos
    self.add_child(power)

# UI界面点击开始按钮触发开始信号
func _on_UI_start_game():
    _nextLevel()

# 创建当前关卡的所有金币
func _spawnCoins():
    if coinScene == null:
        return
    var playerPos = _player.position
    var obstaclePos = _cactus.position
    for i in range(_totalCoins):
        var coin = coinScene.instance()
        var pos = _makeRandomPosition()
        # 如果金币产生位置在玩家或者障碍物内，则重新生成一个位置
        while pos.distance_to(playerPos) < minPlayerDist || pos.distance_to(obstaclePos) < minObstacleDist:
            pos = _makeRandomPosition()
        coin.position = pos
        _coinContainer.add_child(coin)

# 设置当前关卡的障碍物置
func _spawnObstacles():
    var index = randi() % _pointsCurve.get_point_count()
    var position = _pointsCurve.get_point_position(index)
    _cactus.position = position

# 设置能量币出现的时间并计时
func _spawnPowerup():
    var powerTime = _makeRandomPowerAppearTime(_timeLeft)
    _powerTimer.wait_time = powerTime
    _powerTimer.start()

# 根据当前关卡设计金币总数
func _calculateTotal(level):
    return level + 5

# 根据当前关卡设计超时时长
func _calculateDuration(level):
    return level + 5

# 当前时间下设计随机能量出现时间
func _makeRandomPowerAppearTime(timeLeft):
    return rand_range(0, timeLeft)

# 根据窗口尺寸设计随机金币位置
func _makeRandomPosition():
    var x = rand_range(0, ProjectSettings.get('display/window/size/width'))
    var y = rand_range(0, ProjectSettings.get('display/window/size/height'))
    return Vector2(x, y)
```

嗯，这代码有点**长**！当然，这是这个小游戏的核心代码部分了。 `Game.gd` 脚本把主场景中所有的子节点都相互关联在一起，让每个子场景相互配合，工作得有条不紊，另外它还会动态地创建一些其他的子节点，比如金币、能量币等。

代码中的主要逻辑在于处理游戏的开始、暂停、进入下一关卡以及结束等逻辑。对于每个关卡的元素合理设计，比如当前关卡的金币总数、超时时间、能量币的出现时机设计等，*我没怎么用心*，算法不是很合理，如果大家有兴趣，完全可以发挥自己的创造力丰富一下游戏的可玩性吧！嘿嘿。

其他需要注意的代码我在这里列出来：

- `randomize()` 这个方法只需调用一次就可以在每次游戏运行时产生真实的随机效果
- `for coin in _coinContainer.get_children():` 获取该节点的所有子节点（金币）
- `self.get_tree().create_timer(1.5, false)` 创建一个计时器，关键在 `false` 这个参数，表示场景暂停计时同步暂停
- `var position = _pointsCurve.get_point_position(index)` 获取*Path2D* 节点曲线上的某个点的位置值

关于 `yield` 关键字可以在[上一篇文章](https://zhuanlan.zhihu.com/p/51282054)中查看。最后运行游戏，进行测试吧！ :smile:



![img](https://pic2.zhimg.com/80/v2-afd534cc21d0ac8c444bd7f7f455a489_720w.jpg)



## 三、总结

嗯，这个**不好玩**的小游戏总算完成了，总结一下我们的内容：

1. 学习了一些新的 Godot 节点，以及一些新的关键词
2. 探讨了一些基本的游戏开发规则，包括编写代码的规范
3. 编写实现游戏中相关逻辑代码，完成我们第一个完整的小游戏



