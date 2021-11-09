# 写在前面

做Godot 开发 GDScript 是绕不开的内容，所以这个内容必须仔细学习理解。

# GDSCRIPT: GETTING STARTED

## Overview / 概述

Writing scripts and attaching them to nodes and other objects is how you build behavior and game mechanics into your game. For example, a `Sprite` node automatically displays an image, but to move it across the screen, you’ll add a script that tells it how fast, in what direction, and so on.

通过编写脚本并将其附加到节点或者其他的对象中是我们在游戏中建立行为或游戏机制的（常规方法）。例如，一个Sprite（精灵）节点自动的显示一张图片，但是如果需要在屏幕中移动，你需要增加一些脚本去告诉它运动的方向，速度等信息。

You can think of it as the coding version of using the Inspector - GDScript knows all about Godot nodes and how to access them, plus it allows you to change them dynamically.

你可以将其（GDScipt）视为代码版本的 inspector（Godot编辑器中Node的属性设置面板），GCScript 清楚的了解如何访问（或使用）（当前）节点的所有内容，同时允许你去动态的修改他们。

GDScript is Godot’s built-in language for scripting and interacting with nodes. The [GDScript documentation](https://docs.godotengine.org/en/latest/getting_started/scripting/gdscript/gdscript_basics.html) on the Godot website is a great place to get an overview of the language, and I highly recommend taking the time to read through it.

GDScript 是Godot内建的与节点交互的脚本语言。建议你花一些时间通读下Godot网站上的 GDScript 文档中。

**Is GDScript Python?**  / GDScript是Python么 ？

You’ll often read comments to the effect that “GDScript is based on Python”. That’s somewhat misleading; GDScript uses a syntax that’s modeled on Python’s, but it’s a distinct language that’s optimized for and integrated into the Godot engine. That said, if you already know some Python, you’ll find GDScript feels very familiar.

您经常会看到一些关于“GDScript 是基于 Python”的评论。这有点误导；GDScript 使用以 Python 为模型的语法，但它是一种针对 Godot 引擎进行优化并集成到其中的独特语言。也就是说，如果您已经了解一些 Python，您会发现 GDScript 感觉非常熟悉。

Many tutorials (and Godot in general) assume that you have at least *some* programming experience already. If you’ve never coded before, you’ll likely find learning Godot to be a challenge. Learning a game engine is a large task on its own; learning to code at the same time means you’re taking on a lot. If you find yourself struggling with the code in this section, you may find that working through an introductory Python lesson will help you grasp the basics.

许多教程（以及一般的 Godot）假设您已经至少有*一些*编程经验。如果您以前从未编码过，您可能会发现学习 Godot 是一个挑战。学习游戏引擎本身就是一项艰巨的任务；同时学习编码意味着你承担了很多。如果您发现自己在本节中的代码中苦苦挣扎，单独的学习 Python 入门课程将帮助您掌握基础知识会对你带来很多帮助。

## Structure of a script / 脚本的结构

The first line of any GDScript file must be `extends <Class>`, where `<Class>` is some existing built-in or user-defined class. For example, if you’re attaching a script to a `KinematicBody2D` node, then your script would start with `extends KinematicBody2D`. This states that your script is taking all the functionality of the built-in `KinematicBody2D` object and *extending* it with additional functionality created by you.

任何 GDScript 文件的第一行必须是`extends <Class>`，其中`<Class>`是一些现有的内置或用户定义的类。例如，如果您将脚本附加到`KinematicBody2D`节点，那么您的脚本将以`extends KinematicBody2D`. 这表明您的脚本正在使用内置`KinematicBody2D`对象的所有功能，并使用您创建的附加功能对其进行*扩展*。

In the rest of the script, you can define any number of variables (aka “class properties”) and functions (aka “class methods”).

在脚本的其余部分，您可以定义任意数量的变量（也称为“类属性”）和函数（也称为“类方法”）。

## Creating a script / 创建脚本

Let’s make our first script. Remember, any node can have a script attached to it.

让我们制作我们的第一个脚本。请记住，任何节点都可以附加一个脚本。

Open the editor and add a `Sprite` node to empty scene. Right-click on the new node, and choose “Attach Script”. You can also click the button next to the search box.

打开编辑器`Sprite`并向空场景添加一个节点。右键单击新节点，然后选择“附加脚本”。您也可以单击搜索框旁边的按钮。

[![alt](https://kidscancode.org/godot_recipes/img/gds_01_attach.png?width=250)](https://kidscancode.org/godot_recipes/img/gds_01_attach.png?width=250)

Next you need to decide where you want the script saved and what to call it. If you’ve named the node, the script will automatically be named to match it (so unless you’ve changed anything this script will likely be called “Sprite.gd”).

接下来，您需要决定要将脚本保存在何处以及如何调用它。如果您已命名节点，脚本将自动命名以匹配它（因此除非您更改了否则此脚本可能会被称为“Sprite.gd”）。

Now the script editor window opens up, and this is your new, empty sprite script. Godot has automatically included some lines of code, as well as some comments describing what they do.

现在脚本编辑器窗口打开了，这是你新的、空的精灵脚本。Godot 自动包含了一些代码行，以及一些描述它们所做工作的注释。

```gdscript
extends Sprite

# Declare member variables here. Examples:

# var a = 2

# var b = "text"


# Called when the node enters the scene tree for the first time.

func _ready():
    pass # Replace with function body.


# Called every frame. 'delta' is the elapsed time since the previous frame.

#func _process(delta):

#   pass
```

Since the script was added to a `Sprite`, the first line is automatically set to `extends Sprite`. Because this script extends Sprite, it will be able to access and manipulate all the properties and functions that a Sprite node provides.

由于脚本已添加到 a `Sprite`，因此第一行自动设置为`extends Sprite`。由于此脚本扩展了 Sprite，因此它将能够访问和操作 Sprite 节点提供的所有属性和功能。

After that is where you’re going to define all the variables you will use in the script, the “member variables”. You define variables with the ‘var’ keyword - as you can see by the comment examples.

在此之后，您将定义将在脚本中使用的所有变量，即“成员变量”。您可以使用 'var' 关键字定义变量 - 正如您在注释示例中看到的那样。

Go ahead and delete the comments and let’s talk about this next piece.

继续删除评论，让我们看下面的内容。

Now we see a function called `_ready()`. In GDScript you define a function with the keyword “func”. The `_ready()` function is a special one that Godot looks for and runs whenever a node is added to the tree, for example when we hit “Play”.

现在我们看到一个名为`_ready()`. 在 GDScript 中，您可以使用关键字“func”定义一个函数。该`_ready()`函数是一个特殊的函数，每当一个节点被添加到树中时，Godot 就会查找并运行它，例如当我们点击“播放”时。

Let’s say that when the game starts, we want to make sure the Sprite goes to a particular location. In the Inspector, we want to set the *Position* property. Notice that it’s in the section called “Node2D” - that means this is a property that *any* Node2D type node will have, not just Sprites.

假设当游戏开始时，我们要确保 Sprite 转到特定位置。在 Inspector 中，我们要设置*Position*属性。请注意，它在名为“Node2D”的部分中 - 这意味着这是*任何*Node2D 类型节点都将具有的属性，而不仅仅是 Sprite。

How do we set the property in code? One way to find the name of the property is by hovering over it in the Inspector.

我们如何在代码中设置属性？查找属性名称的一种方法是将鼠标悬停在 Inspector 中。

[![alt](https://kidscancode.org/godot_recipes/img/gds_01_01.png)](https://kidscancode.org/godot_recipes/img/gds_01_01.png)

Godot has a great built-in help/reference tool. Click on “Classes” at the top of the Script window and search for Node2D and you’ll see a help page showing you all the properties and methods the class has available. Looking down a bit you can see `position` in the “Member Variables” section - that’s the one we want. It also tells us the property is of the type “Vector2”.

Godot 有一个很棒的内置帮助/参考工具。单击“脚本”窗口顶部的“类”并搜索 Node2D，您将看到一个帮助页面，其中显示了该类可用的所有属性和方法。向下看一点，您可以`position`在“成员变量”部分看到——这就是我们想要的。它还告诉我们该属性的类型为“Vector2”。

[![alt](https://kidscancode.org/godot_recipes/img/gds_01_02.png)](https://kidscancode.org/godot_recipes/img/gds_01_02.png)

Let’s go back to the script and use that property:

让我们回到脚本并使用该属性：

```gdscript
func _ready():
    position = Vector2(100, 150)
```

Notice how the editor is making suggestions as you type. Godot uses vectors for lots of things, and we’ll talk more about them later. For now, let’s type Vector2, and the hint tells us to put two floats for `x` and `y`.

请注意编辑器如何在您键入时提出建议。Godot 在很多事情上使用向量，我们稍后会详细讨论它们。现在，让我们输入 Vector2，提示告诉我们为`x`and放置两个浮点数`y`。

Now we have a script that says “When this Sprite starts, set its position to `(100, 150)`”. We can try this out by pressing the “Play Scene” button.

现在我们有一个脚本，上面写着“当这个 Sprite 启动时，将它的位置设置为`(100, 150)`”。我们可以通过按“播放场景”按钮来尝试一下。

[![alt](https://kidscancode.org/godot_recipes/img/gds_01_03.png)](https://kidscancode.org/godot_recipes/img/gds_01_03.png)

When first learning to code, beginners often ask “How do you memorize all these commands?” It’s not a matter of memorization, it’s about practice. As you use things more, the things you do frequently will “stick” and become automatic. Until then, it’s a great idea to keep the reference docs handy. Use the search function whenever you see something you don’t recognize. If you have multiple monitors, keep a copy of the [web docs](https://docs.godotengine.org/en/latest/) open on the side for quick reference.

刚开始学习编码时，初学者经常会问“你是如何记住所有这些命令的？” 这不是记忆的问题，而是练习的问题。随着你使用的东西越多，你经常做的事情就会“粘”起来，变得自动化。在此之前，最好将参考文档放在手边。每当您看到不认识的东西时，请使用搜索功能。如果您有多个显示器，请保留一份[网络文档](https://docs.godotengine.org/en/latest/) 在侧面打开以供快速参考。

## Wrapping up

Congratulations on making your first script in GDScript! Before moving on, make sure you understand everything we did in this step. In the next part, we’ll add some more code to move the Sprite around the screen. 

恭喜您在 GDScript 中制作了您的第一个脚本！在继续之前，请确保您了解我们在此步骤中所做的一切。在下一部分中，我们将添加更多代码来在屏幕上移动 Sprite。

### Comments