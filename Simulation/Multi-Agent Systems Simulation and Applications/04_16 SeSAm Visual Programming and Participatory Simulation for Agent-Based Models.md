# SeSAm: Visual Programming and  Participatory Simulation for Agent-Based Models

https://multiagentsimulation.com/
---

## 16.1 Introduction

> Agent-based simulation offers a lot of advantages compared to traditional (also microscopic)
approaches, such as elegant representation of heterogeneous populations situated in hetero-
geneous environments, explicit treatment of local effects, or the possibility of formulating
flexible interaction between entities based on intelligent behavior. Agent-based simulation
is becoming more and more popular not only because of these properties. Additionally, it
provides an intuitive and direct form of modeling. Coarsely said, entities observable in the
real world can be described by entities in the virtual world. There is no abstraction step
that necessarily bridges aggregation levels as in macro-simulation.

与传统（也是微观的）方法相比，基于智能体的模拟具有许多优势，例如优雅地表示位于异质环境中的异质种群，
明确处理局部效应，或者基于智能行为在实体之间形成灵活交互的可能性。基于智能体的仿真越来越受欢迎，
不仅仅是因为这些特性。此外，它还提供了一种直观且直接的建模形式。粗略地说，在现实世界中可观察到的实体
可以用虚拟世界中的实体来描述。没有像宏观模拟那样必须桥接聚合级别的抽象步骤。

> As a result, agent-based simulation seems to demand less experience in handling com-
plex mathematics for modeling. Thus, the paradigm of agent-based modeling enables more
researchers to use simulation techniques on their own. Agent-based simulation seems to
be particularly attractive to people that did not use simulation techniques before, nor
received any training in formalizing or programming using traditional programming lan-
guages. Whether agent-based simulation can be widely applied, depends on the availability
of appropriate tools for every level of technical expertise.

因此，基于智能体的模拟似乎在处理用于建模的复杂数学方面需要较少的经验。
因此，基于智能体的建模范式使更多的研究人员能够自行使用仿真技术。
基于智能体的模拟似乎对以前没有使用过模拟技术的人特别有吸引力，
也没有接受过任何使用传统编程语言进行形式化或编程的培训。
基于智能体的仿真是否可以广泛应用，取决于每个技术专业知识级别是否有合适的工具。

> Tools supporting the implementation of agent-based simulations have been developed
since the early 1990’s. In this connection two classes of tools can be identified: class li-
braries on top of a traditional programming language (such as Swarm, www.swarm.org,
accessed June, 2008) or visual programming environments for absolute beginners (such
as AgentSheets, www.agentsheets.com, accessed June, 2008). These early tools merely sup-
ported the implementation of a multi-agent simulation. However, there are more tasks in a
simulation study than only implementing a simulation model. These other tasks, like exper-
imentation, model analysis, etc. were hardly supported. This is still true for many existing
tools, platforms and languages.

自 1990 年代初以来，已经开发了支持基于代理的模拟实施的工具。
在这方面，可以确定两类工具：传统编程语言之上的类库（例如 Swarm，www.swarm.org，2008 年 6 月访问）
或为绝对初学者提供的可视化编程环境（例如 AgentSheets，www.agentsheets.com，2008 年 6 月访问）。
这些早期工具只是支持多智能体模拟的实现。但是，仿真研究中的任务不仅仅是实现仿真模型。
这些其他任务，如经验、模型分析等，几乎不受支持。对于许多现有的工具、平台和语言来说，情况仍然如此。

> In 1995, we introduced the first version of SeSAm (Shell for Simulated Agent Systems).
By this time, SeSAm also focused on supporting implementation providing a high-level
model representation framework. As the linkage to a standard programming language was
different compared to class library-based tools, we had to note that the initial (Lisp-based)
SeSAm was not successful. The reason was mainly that model handling was too complex.
Additionally, for providing model specific add-ons for user participation, experimentation
support, etc. a SeSAm user could not fall back to the basic programming language and add
these tools to the given framework. In 2000/2001 we undertook a complete redesign and
re-implementation of SeSAm using Java, providing more appropriate user support beyond
mere implementation tasks.

1995 年，我们推出了 SeSAm （Shell for Simulated Agent Systems） 的第一个版本。
此时，SeSAm 还专注于支持实现，提供高级模型表示框架。由于与基于类库的工具相比，与标准编程语言的链接不同，
因此我们不得不注意到初始（基于 Lisp）SeSAm 并不成功。原因主要是模型处理太复杂。此外，为了为用户参与、
实验支持等提供特定于模型的附加组件，SeSAm 用户无法退回到基本编程语言并将这些工具添加到给定的框架中。
在 2000/2001 年，我们使用 Java 对 SeSAm 进行了完整的重新设计和重新实现，
提供了更合适的用户支持，而不仅仅是实现任务。

> In this chapter, we introduce SeSAm based on our experiences applying it as well as our
experience supporting others trying to do the same. The rest of the chapter will contain
three parts: at first, a short introduction to the context of human involvement into agent-
based modeling and simulation based on the identification of tasks in a simulation study.
The second part will contain an overview of the SeSAm system and how these different tasks
are supported by it. The third part will contain a short sketch of a number of (partially
interdisciplinary) projects and will discuss our future plans.

在本章中，我们根据我们应用 SeSAm 的经验以及我们支持其他人尝试做同样事情的经验来介绍 SeSAm。
本章的其余部分将包含三个部分：首先，根据模拟研究中任务的识别，简要介绍人类参与基于智能体的建模和模拟的背景。
第二部分将包含 SeSAm 系统的概述以及它如何支持这些不同的任务。第三部分将包含一些（部分跨学科）项目的简短草图，
并将讨论我们的未来计划。

## 16.2 Simulation Study and User Roles

> According to literature, only two or three types of people are typically involved in a simulation 
study: the simulation expert, the system expert, and sometimes a project manager
is mentioned as a third person. We also followed this division of responsibilities in several
projects and also in teaching simulation in interdisciplinary practicals∗. In a greater context,
reuse and maintenance of models have to be considered. This leads to finer considerations
about persons and roles involved in the development and use of simulation models, in general 
and in agent-based simulation models in particular. In the following, we sketch tasks
that may be assigned to specific persons or roles and may be supported appropriately by a
modeling and simulation platform.

根据文献，通常只有两三种类型的人参与仿真研究：仿真专家、系统专家，有时还提到项目经理作为第三人。
我们还在几个项目中遵循了这种职责分工，并在跨学科实践中教授模拟∗。在更大的背景下，必须考虑模型的重用和维护。
这导致了对仿真模型开发和使用中涉及的人员和角色的更精细的考虑，一般而言，特别是在基于智能体的仿真模型中。
在下文中，我们草拟了可以分配给特定人员或角色的任务，这些任务可能会得到建模和仿真平台的适当支持。

## 16.2.1 Tasks and User Roles

> In traditional industrial application domains of simulation – as mostly addressed in introductory 
books like [Law, 2007] – modeling and simulation experts are contracted to construct
and analyze a simulation model for a particular problem or system. There are two to three
different roles involved in such a study: The modeler, the SME “Subject Matter Expert"
and, if necessary, a project manager. A high specialization developed for those application
cases.

在仿真的传统工业应用领域（如 [Law， 2007] 等入门书籍中主要涉及）中，
建模和仿真专家被签约来构建和分析特定问题或系统的仿真模型。
此类研究涉及两到三个不同的角色：建模者、SME“主题专家"，如有必要，还包括项目经理。
为这些应用案例开发的高度专业化。

> In scientific applications such as in social sciences, physics or biology, the system experts
applied simulation for their particular research questions mostly on their own urging for a
different kind of specialized tool or highly specialized (mathematical) expertise.



> In contrast to the two latter cases a sustainable and efficient use, maintenance and reuse
of complex simulation models becomes more and more important to involve new persons
and also systematically support additional tasks. The advent of agent-based simulation
has additionally changed the situation as tasks such as experimentation may become so
demanding that additional persons are required for their execution. Also, the involvement
of human experts without formalization training may be possible in a previously unknown
way. These considerations result in the following set of tasks, in addition to the project
management. We will disregard the latter in the rest of the chapter.


> - **Design of an agent-based simulation model** is the task of developing a concept
    model of the original system that should be analyzed or tested. This step is
    impossible without expertise of the system to be modeled.
> - **Implementation of a computer simulation model** means that the concept model
    is taken and transferred to a programming language in a way that a run-able
    simulation is created.
> - **Observing and controlling** is an activity that is directly connected to implementation
    for testing, analyzing and confirming that the implemented model sufficiently
    corresponds to the conceptual model and to the original system. This is denoted
    here as a specific task, as it should be ideally done or at least supported by people
    not directly involved in model design and implementation.
> - **Observing and immersive testing** denotes another form of testing and validation
    of the implemented model. The persons responsible for these activities should be
    domain experts that can directly evaluate whether the dynamics observed on the
    macro and on the micro level are plausible.
> - **Calibration and experimentation** is a task that involves systematic and thoughtful 
    variation of parameter and input values for finally producing a valid model 
    and making the simulation runs for actual deployment of the model.
> - **Output interpretation** should not be underestimated. This task is directly related
    to the one above. Generated output is interpreted and conclusions are drawn
    as the final result of the simulation study. Also, this task requires deep domain
    knowledge.


- **基于智能体的仿真模型的设计** 是开发应分析或测试的原始系统的概念模型的任务。
  如果没有要建模的系统专业知识，此步骤是不可能的。
- **计算机模拟模型的实现** 意味着概念模型被采用并以创建可运行模拟的方式转移到编程语言中。
- **观察和控制是** 一项与实施直接相关的活动，用于测试、分析和确认实施的模型与概念模型和原始系统充分对应。
  这在这里表示为特定任务，因为理想情况下，它应该由不直接参与模型设计和实现的人员完成或至少提供支持。
- **观察和沉浸式测试** 表示对已实施模型的另一种形式的测试和验证。负责这些活动的人员应该是领域专家，
  他们可以直接评估在宏观和微观层面观察到的动态是否合理。
- **校准和实验** 是一项任务，涉及对参数和输入值进行系统和深思熟虑的更改，以最终生成有效的模型并运行模拟以实际部署模型。
- **输出解释** 不应被低估。此任务与上述任务直接相关。生成的输出被解释并得出结论作为模拟研究的最终结果。
  此外，此任务需要深厚的领域知识。

> It is quite common in many application domains for the model developer, experimenter,
  observer and manager to be one and the same person. In some applications with rather
  industrial backgrounds characterized by long-living models, contracted model development,
  etc. these roles are distributed to a number of people. A consequence can be that a person,
  who is not familiar with the model implementation interface, is responsible for experimenting. 
  Another person just wants to interactively observe the animation.

在许多应用领域中，模型开发人员、实验者、观察者和管理者是同一个人是很常见的。
在一些具有相当工业背景的应用程序中，这些角色以长寿模型、合同模型开发等为特征，
这些角色被分配给许多人。结果可能是不熟悉模型实现接口的人负责实验。
另一个人只想以交互方式观察动画。

> Before continuing with the introduction of a modeling and simulation platform, a short
discussion of user involvement and existing tools is given.

在继续介绍建模和仿真平台之前，本文简要讨论了用户参与和现有工具。

## 16.2.2 User Involvement in Agent-Based Simulation Tools

> Agent-based simulation is particularly apt for involving human users at least for two reasons.

基于代理的模拟特别适合让人类用户参与进来，至少有两个原因。

> Firstly, it forms an intuitive, direct modeling paradigm where the original system is
naturally conceptualized as a collection of actors. A modeler may take the role of such an
actor for specifying its behavior characterizing its rules from the Ego perspective. Therefore,
for conceptualizing and formulating a model no change of the modeling perspective from
micro to macro or from inside to outside the system is necessary. Thus, the direct formulation
of a model is the first reason for intensive involvement of humans that are not experts in
complex particular mathematics. This leads to new implementation frameworks derived
from concepts of visual and end-user programming. Also domain experts can be involved
in the modeling tasks more closely, as the basic model structures are more understandable
than in models based on complex mathematical constructs.

首先，它形成了一个直观、直接的建模范式，其中原始系统自然地被概念化为一组参与者。
建模者可以扮演这样一个参与者的角色，从自我的角度来指定其行为，表征其规则。
因此，要概念化和制定模型，无需将建模视角从微观更改为宏观或从系统内部更改为外部。
因此，模型的直接制定是非复杂特定数学专家的人类深入参与的第一个原因。
这导致了从可视化和最终用户编程概念派生的新实现框架。此外，领域专家可以更密切地参与建模任务，
因为基本模型结构比基于复杂数学结构的模型更容易理解。

> The second reason is also derivable from the possible inside view. Humans may interact
with agents, they may share the perspective, but also may control the model from outside.
Therefore the variety of possible interactions between human user and agent-based simulation
is higher than in macro or abstract simulations where only one level, namely the
aggregated level of observation and parameter manipulation is possible. Additionally the
richness and complexity of the agent behavior makes it interesting for a human to actually
interact with the individual agents.

第二个原因也可以从可能的内景中得出。人类可能会与代理互动，他们可能会共享视角，
但也可以从外部控制模型。因此，人类用户和基于代理的模拟之间可能的交互的种类高于宏观或抽象模拟，
后者只有一个级别，即观察和参数操作的聚合级别是可能的。
此外，代理行为的丰富性和复杂性使人类与各个代理实际交互变得有趣。

> Therefore, user involvement is a theme that has been dealt with since the early 1990’s.
A. Repenning and co-workers coined the term “participatory" theater approach which
combined interactive user interfaces with agent-based simulation [Ambach and Repenning,
1996]. Their ideas were implemented in the end-user programming tool AgentSheets where
visually specified rules for describing agent behavior could be compiled to Java programs
[Repenning et al., 2000]. The main application area of AgentSheets was in children’s games
or educatory simulations, therefore the practical usability for larger models was reduced.
The unstructured set of rules seems to be hardly scalable. Scalability of model representation
was one of the driving ideas behind SeSAm with a structured behavior representation
and regarding features of the visual programming language that enhance scalability.

因此，用户参与是自 1990 年代初以来一直在处理的主题。A. Repenning 及其同事创造了“参与式"剧院方法一词，
它将交互式用户界面与基于代理的模拟相结合 [Ambach 和 Repenning，1996]。他们的想法在最终用户编程工具 
AgentSheets 中实现，其中用于描述代理行为的可视化指定规则可以编译为 Java 程序 [Repenning et al.， 2000]。
AgentSheets 的主要应用领域是儿童游戏或教育模拟，因此降低了大型模型的实际可用性。
非结构化的规则集似乎几乎无法扩展。模型表示的可扩展性是 SeSAm 背后的驱动思想之一，
它具有结构化行为表示以及增强可扩展性的可视化编程语言的功能。

> Kidsim [Smith et al., 1994] and its sucessors were developed for a similar audience like
AgentSheets. They used programming by demonstration for implementing the behavior of
agents. These simulation environments were connected to particular domains and were only
used for interactive simulations for small children. SeSAm was planned as a powerful tool
that allows one to model a broad variety of agent-based models. Nevertheless, learning by
demonstration forms an attractive idea (see Section 16.6).

Kidsim [Smith et al.， 1994] 及其继任者是为与 AgentSheets 类似的受众开发的。
他们使用演示编程来实现代理的行为。这些模拟环境连接到特定领域，仅用于幼儿的交互式模拟。
SeSAm 被规划为一个强大的工具，允许对各种基于智能体的模型进行建模。
尽管如此，通过演示学习形成了一个有吸引力的想法（参见第 16.6 节）。

> During recent years user involvement in agent-based simulation experienced a revival
when role playing games and agent-based simulation were combined, see [Barreteau et al.,
2001] as one of the pioneering works in this area. So-called stakeholder approaches [Moss
and Edmonds, 2005] use the opportunities offered by agent-based simulation as a white-box
approach for intensifying involvement of domain experts, sponsors, etc. Recently, 
participatory involvement of humans’ playing individual agents in a multi-agent simulation were
focussed on by [Guyot and Honiden, 2006]. All these works focus on particular applications,
not on generic tools like SeSAm.

近年来，当角色扮演游戏和基于智能体的模拟相结合时，用户对基于智能体的模拟的参与经历了复兴，
参见 [Barreteau et al.， 2001] 作为该领域的开创性工作之一。
所谓的利益相关者方法 [Moss 和 Edmonds， 2005] 利用基于智能体的模拟提供的机会作为加强领域专家、
发起人等参与的白盒方法。最近，[Guyot 和 Honiden，2006 年] 关注了人类在多智能体模拟中扮演单个代理的参与性参与。
所有这些工作都集中在特定的应用程序上，而不是像 SeSAm 这样的通用工具上。

### 16.2.3 Tools for Agent-Based Simulation in General

> Tools for supporting the development of agent-based simulations have become widely available
 since the mid of 1990’s. Meanwhile a variety of tools can be found, starting from Swarm
as one of the earlier class libraries for developing agent-based simulation. Newer examples
are Repast (*repast.sourceforge.net*, accessed June, 2008) or MASON (*cs.gmu.edu/ eclab/
projects/mason/*, accessed June, 2008) which are basically both class libraries for efficient
event-based simulation. A variety of additional tools are available like GIS-data import,
class libraries for supporting the development of simulation experimentation interfaces, etc.
SeSAm, in contrast to these tools, provides a proprietary language and allows one to im-
plement simulation models without the knowledge of a traditional programming language.

自 1990 年代中期以来，支持基于代理的模拟开发的工具已广泛使用。
同时，可以找到各种工具，从 Swarm 开始，作为开发基于代理的仿真的早期类库之一。
较新的例子是 Repast（repast.sourceforge.net，2008 年 6 月访问）或 
MASON（cs.gmu.edu/ eclab/projects/mason/，2008 年 6 月访问），
它们基本上都是用于基于事件的高效仿真的类库。提供了各种附加工具，如 GIS 数据导入、
用于支持仿真实验接口开发的类库等。与这些工具相比，SeSAm 提供了一种专有语言，
并允许人们在没有传统编程语言知识的情况下实现仿真模型。

> Netlogo (*ccl.northwestern.edu/netlogo/*, accessed June, 2008) is a special, simple programming
 language initially grounded in turtle graphics that allows fast simulations. Meanwhile,
the Hubnet system (*ccl.northwestern.edu/netlogo/hubnet.html*, accessed June, 2008) enhances
 NetLogo for participatory simulations. There are two important differences - SeSAm
provides more elaborate structures for defining the agent behavior and it uses a visual 
programming language.

Netlogo（ccl.northwestern.edu/netlogo/，2008 年 6 月访问）是一种特殊的、简单的编程语言，
最初以图形为基础，允许快速模拟。同时，Hubnet 系统（ccl.northwestern.edu/netlogo/hubnet.html，
2008 年 6 月访问）增强了 NetLogo 的参与式模拟。
有两个重要的区别 - SeSAm 为定义代理行为提供了更复杂的结构，并且它使用了可视化编程语言。

> At the end of the 1990’s, there were attempts to simplify modeling by providing a higher-level
 language built upon general simulation languages, for example MAML for Swarm
[Gulyas et al., 1999], or more recently a new and promising development, Repast Simphony
(repast.sourceforge.net, accessed June, 2008). It aims at facilitating modeling and simulation
by providing appropriate user interfaces allowing the generation of Java code to GUI-based
control of simulations. In contrast to this, SeSAm models are accessible using visual interfaces
 at any stage of use. An additional – also specification-level programmed – user
simulation interface builder allows also to produce model-specific dialogs.

在 1990 年代末，有人尝试通过提供基于通用仿真语言构建的更高级别的语言来简化建模，
例如 MAML for Swarm [Gulyas et al.， 1999]，或者最近的一个新的有前途的开发项目 
Repast Simphony（repast.sourceforge.net，2008 年 6 月访问）。
它旨在通过提供适当的用户界面来促进建模和仿真，从而允许生成 Java 代码以基于GUI的仿真控制。
与此相反，SeSAm 模型可以在任何使用阶段使用可视化界面访问。一个额外的 - 也是规范级编程的 - 
用户模拟界面构建器也允许生成特定于模型的对话框。

> In addition to a survey on simulation engines for agent-based simulation [Theodoropoulos
et al., 2008], this book also contains a chapter about JAMES II [Himmelspach and R¨ohl,
2008]. This particular simulation framework separates an explicit model specification from
the executable model automatically converted to Java code.

除了对基于智能体的仿真的仿真引擎的调查 [Theodoropoulos et al.， 2008] 之外，
本书还包含关于 JAMES II 的章节 [Himmelspach 和 R ̈ohl， 2008]。
这个特定的仿真框架将显式模型规范与自动转换为 Java 代码的可执行模型分开。

> For several years, commercial tools for agent-based simulation have also been available.
An example for a general tool is AnyLogic (www.xjtek.com, accessed June, 2008). It provides
modeling support for different modeling paradigms: agent-based modeling and event-based
models as well as system dynamics models that can also be combined in one model. Although
the basic agent behavior definition is based on statecharts, most items of the modeling
interface connect directly to Java code. In SeSAm, Java code is completely hidden.

几年来，用于基于智能体的仿真的商业工具也已经面世。通用工具的一个例子是 AnyLogic（www.xjtek.com，2008 年 6 月访问）。
它为不同的建模范式提供建模支持：基于智能体的建模和基于事件的模型，以及也可以组合在一个模型中的系统动力学模型。
尽管基本代理行为定义基于状态图，但建模接口的大多数项都直接连接到 Java 代码。在 SeSAm 中，Java 代码是完全隐藏的。

> In particular domains specialized commercial tools for Agent-based simulations can be
bought. An example is SimWalk for agent-based pedestrian simulations (www.simwalk.ch,
accessed June, 2008). SeSAm also has been used for pedestrian simulation; the pedestrian
behavior can be manipulated allowing for flexible reactions to perceptions of local congestions,
etc. In SimWalk, the agent behavior is fixed, only origin and destination areas and
other input value configuration can be defined. This makes it useful for standard 
applications, yet inhibits research.

特别是，可以购买用于基于 Agent 的模拟的专用商业工具。一个例子是用于基于代理的行人模拟的 
SimWalk（www.simwalk.ch，2008 年 6 月访问）。SeSAm 也已用于行人模拟;行人的行为可以纵，
从而对当地拥堵等的感知做出灵活的反应。在 SimWalk 中，代理行为是固定的，只能定义起点和终点区域以及其他输入值配置。
这使得它对标准应用很有用，但抑制了研究。

> Platforms and programming languages for developing agent systems may also be used
for implementing agent-based simulation models. This can be done by adding a simulation
time service to an agent platform [Braubach et al., 2006], or directly using specific agent
programming languages like Jason [Bordini and H¨ubner, 2008] which is also shown in this
book. The latter offers a powerful, well-structured formal language for programming agents.
In addition to its focus on simulation, SeSAm is based on a more practical approach.

用于开发代理系统的平台和编程语言也可用于实现基于代理的仿真模型。这
可以通过向代理平台添加模拟时间服务 [Braubach et al.， 2006] 或直接使用特定的代理编程语言来完成，
如 Jason [Bordini 和 H ̈ubner， 2008]，这在本书中也有展示。
后者为编程代理提供了一种功能强大、结构良好的正式语言。除了专注于仿真之外，SeSAm 还基于一种更实用的方法。

> At the Department of Artificial Intelligence and Applied Computer Science at the 
University of W¨urzburg, we developed a modeling and simulation environment named SeSAm that
combines concepts of declarative high-level model representation and visual programming.
The initial aim behind our efforts was similar to the idea of AgentSheets of providing a tool
for beginners in modeling and programming. However, our intention was more ambitious as
we wanted to develop a scalable platform that can be used for real-world applications. Thus,
we also wanted to develop a modeling and simulation system apt for rapid-prototyping by
experts. In the remainder of this chapter, we will describe the modeling and simulation
system of SeSAm with a focus on the new developments concerning user tasks and their
support. Finally we will discuss some anecdotic, yet symptomatic experiences we made when
applying SeSAm.

在维尔茨堡大学人工智能与应用计算机科学系，我们开发了一个名为 SeSAm 的建模和仿真环境，
它结合了声明性高级模型表示和可视化编程的概念。我们努力的最初目标类似于 AgentSheets 的想法，
即为建模和编程的初学者提供工具。然而，我们的意图更加雄心勃勃，因为我们想开发一个可用于实际应用的可扩展平台。
因此，我们还希望开发一个适合专家快速原型制作的建模和仿真系统。在本章的其余部分，我们将描述 SeSAm 的建模和仿真系统，
重点介绍有关用户任务及其支持的新发展。最后，我们将讨论我们在应用 SeSAm 时所做的一些轶事但有症状的经历。


## 16.3 Core SeSAm
> In this chapter we want to describe SeSAm, a modeling and simulation environment that
was constructed to support as many of the above sketched tasks as possible. SeSAm basically
provides a platform for implementing and experimenting with agent-based simulation
models using a higher level modeling language. Starting with some core facilities, it was stepwise
enhanced to its current status. Currently SeSAm contains several components whose
relations are depicted in Figure 16.1.

在本章中，我们想描述 SeSAm，这是一个建模和仿真环境，旨在支持尽可能多的上述草图任务。
SeSAm 基本上提供了一个平台，用于使用更高级别的建模语言实现和试验基于智能体的仿真模型。
从一些核心设施开始，逐步提升到现在的状态。目前 SeSAm 包含几个组件，其关系如图 16.1 所示。

> ![img_34.png](img_34.png)
> FIGURE 16.1 Overview of the SeSAm system: Based on the high-level model representation, several
modules are built that allow to implement the model and its instrumentation (“Analysis Routines") 
conveniently using visual programming (“Visual Modeling"). The model given in the representation language is
interpreted (“Interpreter") and put into a dynamic context for simulation (“Simulator"); The output data
can be automatically animated (“Animation") or stored into files for later analysis (“Protocol data"). 
Visual programming can also be used to generate specific user interfaces for the simulation runs (“Interactive
Frontend"). All these modules are based on the given model representation.
> 
> 图 16.1 SeSAm 系统概述：基于高级模型表示，构建了几个模块，
> 这些模块允许使用可视化编程（“可视化建模 / Visual Modeling"）方便地实现模型及其工具（“分析例程 / Analysis Routines"）。
> 以表示语言给出的模型被解释（“解释器 / Interpreter"）并放入动态上下文中进行模拟（“模拟器/Simulator"）;
> 输出数据可以自动进行动画处理（“动画 / Animation"）或存储到文件中以供以后分析（“协议数据/Protocol data"）。
> 可视化编程还可用于为仿真运行生成特定的用户界面（“交互式前端 / Interactive Frontend"）。所有这些模块都基于给定的模型表示。

> SeSAm is based on a specific, proprietary language for describing the elements of a
multi-agent model: from the basic elements of the model, namely the structure and dynamics of
agents and their environment to possible configurations, instrumentation and experiment
description. Due to its declarative character there is a clear separation between model and
simulator. All elements of the model description can be entered into the SeSAm system
using visual programming. There are also facilities for importing data from databases, 
tables/spreadsheets, GIS- and CAD files, etc.

SeSAm 基于一种特定的专有语言来描述多智能体模型的元素：从模型的基本元素，
即智能体的结构和动态及其环境到可能的配置、仪器和实验描述。
由于其声明性特性，模型和模拟器之间有明显的区别。模型描述的所有元素都可以使用可视化编程输入到 SeSAm 系统中。
还有一些工具用于从数据库、表格/电子表格、GIS 和 CAD 文件等导入数据。

> The model description is compiled into some corresponding, yet partially more efficient
representation that is interpreted for actually producing model dynamics in a simulation.
Due to the explicitness of the language, there are in-built facilities for animation, data
gathering and visualization based on model-specific selected protocol data. Recently, the system
has been enhanced by a tool that allows building specific user interfaces for interactive
simulation, as well as a possibility to control agents from outside the simulation. All the
modules depicted in Figure 16.1 will be discussed later in this chapter after the introduction
of the model representation language on which they are based.

模型描述被编译成一些相应的，但部分更有效的表示形式，这些表示形式被解释为在模拟中实际生成模型动力学。
由于该语言的明确性，有基于特定于模型的选定协议数据的内置动画、数据收集和可视化工具。
最近，该系统通过一种工具得到了增强，该工具允许为交互式仿真构建特定的用户界面，以及从仿真外部控制代理的可能性。
图 16.1 中描述的所有模块都将在本章后面介绍它们所基于的模型表示语言之后进行讨论。

### 16.3.1 Basic Model Representation

> The high-level modeling language of SeSAm consists of elements on different levels 
> as depicted in Figure 16.2.

SeSAm 的高级建模语言由不同级别的元素组成，如图 16.2 所示。

> ![img_35.png](img_35.png)
> FIGURE 16.2 Building blocks of the SeSAm language: the atomic elements of the model representation
  are the primitives that form the basic elements of all descriptions of actions, perceptions where actual
  modifications happen. The concretely specified primitive calls are used for characterizing the dynamics of
  the agents, resources and also the world. Additionally, these entities are characterized by a structure that is
  able to capture their status. Based on this core model, additional information is integrated for specifying a
  fully functional model: Specifications of configuration (possible start situations) and of routines for collecting
  data to export in protocols. All this information is integrated into a full simulation run specification. The
  latter can be augmented by an interface declaration or several of them can be aggregated to experiments.
> 
> 图 16.2 SeSAm 语言的构建块：模型表示的原子元素是构成所有动作描述的基本元素的基元，
> 这些感知发生在实际修改的地方。具体指定的 primitive calls 用于描述代理、
> 资源以及世界的动态。此外，这些实体的特征是能够捕获其状态的结构。
> 基于此核心模型，集成了其他信息以指定功能齐全的模型：配置规范（可能的启动情况）和用于收集数据以在协议中导出的例程。
> 所有这些信息都集成到一个完整的仿真运行规范中。后者可以通过接口声明进行扩充，或者将其中的几个可以聚合到实验中。

> - *Primitives and data structures* form the basic language elements like in any other
    programming language. Primitives and data structures may be built-in or
    user-defined. The latter are saved together with the complete description as XML
    file.
> - *Static structures* are the description of the structural composition of the system:
    entity and environment classes, state variables and their domains describing the
    entities’ bodies, etc.
> - *Configuration* of the initial situations including descriptions of a number of
    instances and start values for each instance, its positions, etc.
> - *Description of dynamic reasoning* as the specification of agent and environmental
    behavior.
> - *Meta-level characterization* means basically descriptions of what to do with the
    model: experiment scripts, model instrumentation, visualization, etc.

- *基元和数据结构* 构成了基本语言元素，就像任何其他编程语言一样。 
  基元和数据结构可以是内置的，也可以是用户定义的。后者与完整描述一起保存为 XML 文件。
- *静态结构* 是对系统结构构成的描述：实体和环境类、描述实体主体的状态变量及其域等。
- "配置* 是指初始状态，包括实例数量和每个实例的起始值、其位置等的描述。
- *动态推理描述* 为代理和环境行为的规范。
- *元级表征* 基本上是指对模型处理什么的描述：实验脚本、模型检测、可视化等。

> In the remainder of this section, we will sketch the essentials of each of these language elements.

在本节的其余部分，我们将概述这些语言元素的基本要素。

#### Model Level

***Primitives, User Functions and Data Types***  
***基元、用户函数和数据类型*** 

> So-called *primitives* form the basic building blocks of the model and connect the model
to the basic programming language: internally, every primitive consists of two parts: a 
declaration part and a Java method named *execute*. The declaration part contains a structured
description of input and output argument types together with some text that describes
its functionality. This information is parsed by the SeSAm system for generating the basic
parts of the visual interface.

所谓的*基元*构成了模型的基本构建块，并将模型连接到基本编程语言：在内部，每个原语都由两部分组成：
声明部分和名为 execute 的 Java 方法。声明部分包含输入和输出参数类型的结构化描述以及一些描述其功能的文本。
此信息由 SeSAm 系统解析，以生成可视界面的基本部分。

> There are different categories of primitives:

基元有不同类别的：

> - *Action Primitives* are the actions that an agent may exert for manipulating its
    status or its environment. These primitives are connected to Java methods that
    modify the agent or its environment specified by the arguments given to the
    action. Examples are move or setVariable.
> - *Sensor Primitives* collect information from the agent’s environment and also
    from its internal state. An example is a primitive that returns a list of objects
    that the agent is able to perceive in some direction within some range,
    like observeAllObjectsInDirection.
> - *Computational Primitives* form a quite heterogeneous set of functions that provide
    means for the agents to execute more or less complex computations based
    on the sensor information and parameters of their behavioral program. An
    example is the calculation of the heading of the agent using some simple position
    mathematics. Other examples are comparison predicates, list manipulation, etc.

- *行为基元（Action Primitives）* 是代理为操纵其状态或环境而可以执行的操作。
  这些基元连接到 Java 方法，这些方法修改代理或其环境，这些环境由给定给操作的参数指定。
  例如 move 或 setVariable。
- *传感器基元（Sensor Primitives）* 从代理的环境及其内部状态收集信息。
  例如，一个基元返回一个对象列表，代理能够在某个范围内的某个方向上感知这些对象，
  例如 observeAllObjectsInDirection。
- *计算基元 （Computational Primitives）* 形成一组相当异构的函数，
  这些函数为代理提供了根据其行为程序的传感器信息和参数执行或多或少复杂计算的方法。
  一个例子是使用一些简单的位置数学计算代理的航向。其他示例包括比较谓词、列表操作等。

> We provided a set of primitives that can be shown to be Turing-complete [Oechslein, 2003].
A modeler may define complex nested calls of primitives as macros called *user primitives*.
These macros provide abstractions in the sense of model-specific functions. The following
excerpt from a SeSAm model xml file shows the definition of such a user function in a
simple predator-prey model. It contains the definition of a flee action of a prey agent
toward a shelter `simObject` that is computed in another user function addressed by calling
`UserFunction0`. The user function possesses only one argument, namely the active agent
itself. The return value is void denoting that it is an action.

我们提供了一组可以证明是图灵完备的基元 [Oechslein， 2003]。
建模者可以将基元的复杂嵌套调用定义为称为*用户基元*的宏。
这些宏提供特定于模型的函数意义上的抽象。以下摘自 SeSAm 模型 xml 文件显示了简单 
predator-prey 模型中此类用户函数的定义。它包含猎物代理对庇护所 simObject 的逃跑动作的定义，
该动作在另一个用户函数中计算，通过调用 UserFunction0 寻址。
user 函数只有一个参数，即 active agent 本身。返回值为 void，表示它是一个操作。

```xml
...
<userFunction name="Flee from predator" id="UserFunction1" external="true" expert="false" inline="true">
    <functionCall>
        <call functionName="MoveTowardsPos">
            <call functionName="GetSpatialInfo">
                <parameterID id="FunctionArgument1"/>
            </call>
            <call functionName="GetPosition">
                <call functionName="GetSpatialInfo">
                    <call userFunctionID="UserFunction0">
                        <parameterID id="FunctionArgument1"/>
                    </call>
                </call>
            </call>
            <call functionName="GetSpeed">
                <call functionName="GetSpatialInfo">
                    <parameterID id="FunctionArgument2"/>
                </call>
            </call>
        </call>
    </functionCall>
    <parameter name="ich" id="FunctionArgument1">
        <simObjectType/>
    </parameter>
    <voidType/>
</userFunction>
...
```
> The SeSAm modeling language provides a priori a set of atomic and abstract data types
ranging from boolean, numbers, etc. to lists or hashtables. Composed data types and
enumerations may be added by a modeler to provide model-specific types and abstractions in
a similar way to user primitives

SeSAm 建模语言提供了一组先验的原子和抽象数据类型，范围从布尔值、数字等到列表或哈希表。
建模者可以添加组合数据类型和枚举，以类似于用户基元的方式提供特定于模型的类型和抽象



***Structural Description***
***结构描述***

> There are different structural elements and levels built upon these basic primitives. An
overview can be found in Figure 16.3.

在这些基本基元上构建了不同的结构元素和级别。图 16.3 中提供了概述。

> ![img_36.png](img_36.png)
> FIGURE 16.3
Basic structure for describing the structural building blocks of a SeSAm model: There are
three different types of entities all derived from the `simObject` class: `Resources` that represent static
objects that can be manipulated, `agents` that possess also a behavior descriptions and the world that
additionally may contain other global representations such as a map. The `simObject` structure that is
responsible for storing the current status of an entity. This status is stored in a collection of state variables
that together form the entities “body“.
>
> 图 16.3 描述 SeSAm 模型结构构建块的基本结构：有三种不同类型的实体都源自 simObject 类：
> 表示可操作的静态对象的资源、还具有行为描述的代理以及可能还包含其他全局表示（如地图）的世界。
> 负责存储实体当前状态的 simObject 结构。此状态存储在状态变量的集合中，这些变量共同构成实体 “body“。

> A multi-agent model consists here of a set of models of entities – in the terminology
of SeSAm simObjects. Their structure and behavior is described on the class description
level. Individual entities are characterized at the configuration or instance description level.
For the simulation, actual object instances are generated from these instance descriptions.
This three-level system of description allows one to separate explicitly between model and
simulation run, enabling the visual programming facilities of SeSAm (see Section 16.4.3)
and allowing one to add an additional compilation step for generating simulation entities
from instance descriptions.

多智能体模型由一组实体模型组成 – 用 SeSAm simObjects 的术语来说。
它们的结构和行为在 类描述 级别上描述。单个实体在配置或实例描述级别进行表征。
对于模拟，实际对象实例是根据这些实例描述生成的。这个三级描述系统允许在模型和仿真运行之间显式分离，
启用 SeSAm 的可视化编程工具（参见 Section 16.4.3），并允许添加额外的编译步骤，以便从实例描述生成仿真实体。

> For reasons of model clarity, there are three specific different kinds of object class 
descriptions, derived from the generic simObject class description:
> - **Agent class** descriptions form the basis for all model-specific agent classes: for
    example a Pedestrian Class or an Ant Class is basically an instance of an agent
    class description. A basic agent class description consists of a characterization of
    its body and its behavior.
> - **Resource class** descriptions are used for integrating static entities populating the
    environment of the agents. They just contain some status that may be manipulated
    and accessed by the agents.
> - **World class** descriptions are basically special agent class descriptions that contain
    global status variables or parameter. They enable formulation of some global level
    behavior. Therefore on the configuration instance level only one unique instance
    of a model-specific world class is allowed per situation (see below).

为了明确模型，有三种特定的不同类型的对象类描述，这些描述源自通用 simObject 类描述：
- **代理类**描述构成了所有特定于模型的代理类的基础：例如，Pedestrian Class 或 Ant Class 基本上是代理类描述的实例。
  基本的 agent 类描述包括其主体及其行为的特征。
- **资源类**描述用于集成填充代理环境的静态实体。它们只包含一些可能被代理操作和访问的状态。
- **World 类**描述基本上是包含全局状态变量或参数的特殊 Agent 类描述。
  它们支持制定某些全局级别的行为。因此，在配置实例级别上，每种情况只允许一个特定于模型的世界级的唯一实例（见下文）。

> All simObject class descriptions contain declarations as to how the status of their
instances is represented. In the current SeSAm version the container for all status information
or individual parameter etc. is characterized as “body". The body consists of a set of
variables and constants. A body description is associated with a class description. Thus, this
body structure also mirrors the three levels of class description, instance and actual 
entity by body description, body instance description and actual body, the latter only exists
during a simulation run.

所有 simObject 类描述都包含有关如何表示其实例状态的声明。在当前的 SeSAm 版本中，
所有状态信息或单个参数等的容器都被描述为 “body”。主体由一组变量和常量组成。
正文描述与类描述相关联。因此，此 body 结构还通过 body description、body 实例描述和实际 body 反映了类描述、
实例和实际实体的三个级别，后者仅存在于模拟运行期间。

> Variables – also on corresponding description layers – are characterized by the following
information:
> - Name of the variable
> - Data Type (boolean, number, string, list, hashtable, pointer to simObject, but
    also position, shape, image,...)
> - Characterization: configuration parameter, state variable, output variable or
    supporting variable.
> - Default initial value
> - Interface characterization denoting whether its value is perceivable or even
    manipulate for other agents

变量 – 也位于相应的描述层上 – 由以下信息表征：
- 变量的名称
- 数据类型（布尔值、数字、字符串、列表、哈希表、指向 simObject 的指针，以及位置、形状、图像,...）
- 特征：配置参数、状态变量、输出变量或支持变量。
- 默认初始值
- 界面特性，表示其值是否可感知，甚至是否为其他代理所操纵

> Variables may be grouped in so called “features“ which can be assigned to more than
one simObject class. Combined with user primitives that specifically work on those feature
variables these language elements provide common abilities to agent, resource and the world
classes. This might be useful for model elements that deal with identifiers or different types
of memory, etc. Features also form the basis of an important plugin-mechanism which will
be described in more detail in Section 16.3.3.

变量可以分组为所谓的 “特征“ ，这些 “特征“ 可以分配给多个 simObject 类。
结合专门处理这些特征变量的用户原语，这些语言元素为 agent、resource 和 world 类提供了通用功能。
这对于处理标识符或不同类型内存等的模型元素可能很有用。
功能也构成了一个重要的插件机制的基础，这将在 Section 16.3.3 中更详细地描述。

> There are several predefined features that additionally provide specific data types. The
most prominent feature-level plugins are spatial representations. The standard one is a
continuous 2d space consisting of a feature for the environment that provides a map description
at the world instance description level and a concrete map for the actual world instance, as
well as variables containing the spatial information of an entity for the agent and resource
classes on the different levels of declaration. Spatial information for the 2d continuous case
contains not only position, but also shape in form of a polygon, speed, direction and in-
formation about visualization like color, image,... This feature also encapsulates specific
primitives for spatial perception as well as several movement primitives. The treatment
of spatial information as feature has the advantage of flexibility: only entities – resources
or agents that possess the spatial information feature are positioned on the map. These
entities may be combined with non-spatial agents like abstract, non-spatial agents, for
example organizational agents. By exchanging this feature assignment, other forms of spatial
representation can be used without any changes on the platform level or even concurrently.

还有几个预定义功能，它们还提供了特定的数据类型。最突出的要素级插件是空间表示。
标准空间是一个连续的 2D 空间，由环境特征组成，该功能在世界实例描述级别提供地图描述，
为实际世界实例提供具体地图，以及包含不同声明级别上的代理和资源类的实体空间信息的变量。
2D 连续情况的空间信息不仅包含位置，还包含多边形形式的形状、速度、方向和有关可视化的信息，
如颜色、图像,...此功能还封装了用于空间感知的特定基元以及多个运动基元。
将空间信息视为特征具有灵活性的优势：只有实体 – 具有空间信息特征的资源或代理才会定位在地图上。
这些实体可以与非空间代理（如抽象、非空间代理）相结合，例如组织代理。
通过交换此要素分配，可以使用其他形式的空间表示，而无需在平台级别进行任何更改，甚至无需同时进行任何更改。

***Behavior Description***
***行为描述***

> Using the above introduced primitives, dynamics can be expressed similarly to traditional
programming languages. However, SeSAm provides language constructs for organizing the
description of behavior of agents and of the world:

使用上面介绍的基元，动态可以像传统编程语言一样表示。但是，SeSAm 提供了用于组织代理和世界行为描述的语言结构：

> The behavior description is inspired by UML activity diagrams: consisting of activity
nodes and arrows that depict transition rules between activities. Special activities are the
start and the end activity. When the behavior of the agent ends up in the end node, the
agent is deleted from the simulation. When an agent is generated, the interpretation of the
activity diagram starts at the start node.

行为描述的灵感来自 UML 活动图：由描述活动之间转换规则的活动节点和箭头组成。
特殊活动是 start 和 end 活动。当代理的行为最终出现在终端节点中时，该代理将从模拟中删除。
生成代理时，活动图的解释从起始节点开始。

> An agent (as well as the world entity) may have arbitrary many activity graphs or 
“reasoning engines” as they are called in the SeSAm terminology. This allows the modeler
formulating concurrent behaviors performed by one agent – for example defining negotiation
behavior in one reasoning engine and concurrent manipulation of the environment in
another.

代理（就是世界实体）可以具有任意数量的活动图或“推理引擎“，它们在 SeSAm 术语中称为。
这允许建模者制定由一个代理执行的并发行为 —— 例如，在一个推理引擎中定义协商行为，
在另一个推理引擎中定义环境的并发操作。

> An activity encapsulates three sequences of actions that are basically sequences nested
primitive calls: **start actions** that are performed when the activity is selected anew, **standard
actions** that are performed once every time step as long as the agent is executing that activity
and **termination actions** that are executed for cleaning up when the agent has decided to
change its activity.

一个活动封装了三个操作序列，这些操作基本上是嵌套基元调用序列：
- **start actions** 重新选择活动时启动执行的操作，
- **standard actions** 只要代理执行该活动，每个时间步执行一次的标准操作
- **termination actions** 当代理决定更改其活动时为清理而执行的终止操作。


> Rules are responsible for terminating one activity and selecting the next. They are linked
to their predecessor activity and tested every time this activity is executed by an agent. Rules
may contain arbitrarily nested function calls of primitives finally returning a boolean value
as pre-conditions and an activity as post-condition. A special kind of rule has “otherwise“
as condition which means that this rule fires if the condition of no other rule associated
with the same activity returns true. With this special rule a sequence of activities can be
enforced without detailed implementation of further conditions. Conflict resolution in the
case of more than one applicable standard rule is random selection. There are two types of
activity concerning their temporal aspects: “instant“ or “time consuming“ activities. The
basic update cycle is round-based (see Section 16.3.2). This label denotes at which activity
the rule-based selection and execution cycle stops waiting for the next update signal.

规则负责终止一个活动并选择下一个活动。它们链接到其前置活动，并在代理每次执行此活动时进行测试。
规则可以包含基元的任意嵌套函数调用，这些基元最终返回布尔值作为前提条件，并返回活动作为后置条件。
特殊类型的规则将 “else“ 作为 condition，这意味着如果与同一活动关联的没有其他规则的条件返回 true，
则会触发此规则。使用此特殊规则，可以强制执行一系列活动，而无需详细实施其他条件。
如果存在多个适用的标准规则，则冲突的解决方式是随机选择。就其时间方面而言，
有两种类型的活动：“即时“或“耗时“活动。基本更新周期是基于轮次的（请参阅 Section 16.3.2）。
此标签表示基于规则的选择和执行周期在哪个活动停止等待下一个更新信号。


> Activity graphs can become quite large and thus, without further structuring means,
hard to conceive by a human modeler. Therefore additional language-level support is given
by introducing hierarchical composition of activities. A partial graph can be replaced by a
composed activity, without any change in the interpretation of the overall activity graph.
Rules selecting an activity within this new graph are simply routed via the start node of
the partial graph. Similarly, rules selecting activities outside of the composed activity graph
are routed via the end node. Both start and end node are interpreted as instant activities
without time consumption.

活动图可能会变得非常大，因此，如果没有进一步的结构化手段，人类建模者很难想象。
因此，通过引入活动的分层组合来提供额外的语言级支持。部分图可以替换为组合活动，
而不会对整个活动图的解释发生任何变化。在此新图表中选择活动的规则只需通过部分图表的起始节点进行路由即可。
同样，选择组合活动图之外的活动的规则将通过结束节点路由。开始节点和结束节点都被解释为即时活动，不会消耗时间。

***Declaration of Situations***
***声明状况***

>As mentioned before, there is an additional description level between the agent, resource
or world class and a simulation run: descriptions of possible model configuration or
“situation" declarations as they are called in the SeSAm terminology. The description of a
situation contains a set of instance descriptions. There may be arbitrary many agent or
resource instance declarations, but only one unique instance of a world class. The reason is
obvious when keeping in mind that the world instance represents the global aspects of the
environment.

如前所述，代理、资源或世界级与模拟运行之间还有一个额外的描述级别：
可能的模型配置或 SeSAm 术语中称为“状况"声明的描述。状况描述包含一组实例描述。
可以有任意多个代理或资源实例声明，但只有一个世界级的唯一实例。
请记住，世界实例表示环境的全局方面，原因很明显。

> An instance description mainly contains – in addition to a pointer to the behavior
description – a body instance description with a set of variable instance descriptions. There
the important aspect is the individualization of initial values for the variables. In models
with explicit spatial representations, on this level the map declaration – as an instance of
the spatial feature class assigned to the world class – is available that allows for localization
of entities that possess the spatial information feature.

除了指向行为描述的指针外，实例描述还主要包含一个 body 实例描述和一组可变实例描述。
其中重要的方面是变量初始值的个性化。在具有显式空间表示的模型中，在此级别上，
地图声明（作为分配给 world 类的空间要素类的实例）可用，它允许对具有空间信息特征的实体进行定位。

> For facilitation of situation designs with many elements, we integrated groups of instances
that can be named as a group and used as a template for partial situation configurations.

为了促进具有许多元素的情境设计，我们集成了实例组，这些实例组可以命名为一个组，并用作部分情境配置的模板。

#### Experiment Description Level / 实验描述级别

> With the declaration of a situation the model itself is completely specified. However, for
being able to perform useful simulation experiments additional information has to be provided.

通过情况的声明，模型本身被完全指定。但是，为了能够执行有用的仿真实验，必须提供额外的信息。

***Declaration of Model Instrumentation***
***模型仪表生命***

>The most important point is the definition of measurements that can be taken from
the agent-based simulation. These can be variables defined in the world class, where data
may be aggregated for protocol, but also specific output variables of prominent agents.
Model instrumentation is provided from outside the model and should not be a part of
the core model. Therefore, specific measurements may be explicitly defined and added to a
situation description. The declaration of model instrumentation may contain primitive calls
for collecting the necessary information from the multi-agent system and information on
what should be done with this gathered information. Basically two options are available:
writing the data to protocol files or visualization in different forms of diagrams that animate
the changes throughout the simulation run.

最重要的一点是可以从基于智能体的模拟中获取的测量的定义。这些可以是 world class 中定义的变量，
其中数据可以针对协议进行聚合，也可以是著名代理的特定输出变量。模型插桩是从模型外部提供的，
不应成为核心模型的一部分。因此，可以明确定义具体的测量并添加到情况描述中。
模型插桩的声明可能包含用于从多代理系统收集必要信息的基元调用，以及有关如何处理这些收集到的信息的信息。
基本上有两个选项可用：将数据写入协议文件或以不同形式的图表可视化，在整个仿真运行过程中为变化添加动画效果。

***Simulation Run Definition and Experiment Declaration***
***仿真运行定义和实验声明***

> A simulation run contains not only the initial description of the situation and the
instrumentation of the run. It additionally contains the description of a condition for 
terminating the simulation run. This condition may access the simulation time or may be a 
characteristic of the complete situation, for example when all agents have been deleted.

仿真运行不仅包含情况的初始描述和运行的检测。它还包含终止模拟运行的条件的描述。
此条件可能会访问模拟时间，也可能是完整情况的特征，例如，当所有代理都已被删除时。

> Several simulation runs can be aggregated to experiments. Instead of providing some
predefined framework for describing variations of parameter values and corresponding
simulation runs, we decided to provide full programming power for experiments. It allows
scripting simulation runs with full flexibility. For this aim, primitives operating on
situation declarations, setting the random seed, generating and executing simulation runs are
provided.

可以将多个模拟运行聚合到试验中。我们决定为实验提供完整的编程功能，
而不是提供一些预定义的框架来描述参数值的变化和相应的仿真运行。
它允许以完全的灵活性编写模拟运行脚本。为此，提供了对情况声明进行操作、
设置随机种子、生成和执行仿真运行的原语。

### 16.3.2 Simulation Routine and Model Interpretation / 仿真例程和模型解释

> Up to now, we briefly sketched the full model and simulation description language used
by SeSAm. The semantics of the higher level elements are given by the interpreter, the
semantics of the primitives by the underlying Java code. There is a compilation step between
model description and simulation run for two reasons:
> 1. Clear separation between model and simulation
> 2. Possible code optimization based on techniques from compiler design, like
     constant folding, code in-lining, etc. These optimization steps are transparent for
     the user. They enable SeSAm to execute simulation runs rather fast.

到目前为止，我们简要概述了 SeSAm 使用的完整模型和仿真描述语言。
更高级别元素的语义由解释器给出，基元的语义由底层 Java 代码给出。
模型描述和仿真运行之间存在编译步骤，原因有两个：

1. 模型和仿真之间的明确分离
2. 基于编译器设计中的技术（如常量折叠、代码内联等）的可能代码优化。
   这些优化步骤对用户是透明的。它们使 SeSAm 能够相当快速地执行仿真运行。

> ![img_37.png](img_37.png)
> FIGURE 16.4 Interpretation cycle of SeSAm: After an update of the unique world entity, 
> all agents are updated in a random sequence. Then, the world may again update, etc.
> 
> 图 16.4 SeSAm 的解释周期：在更新唯一世界实体后，所有代理都以随机顺序更新。然后，世界可能会再次更新，依此类推。

####  Basic Information about the Simulator / 模拟器的基本信息

> SeSAm provides a round-based simulation where the agents are updated one after the other
in a random sequence. When all agents are treated, the world entity will be updated, thus
the update of the world is the only possible synchronization point within one update round.

SeSAm 提供基于轮次的模拟，其中代理以随机顺序一个接一个地更新。
当处理所有代理时，世界实体将被更新，因此世界的更新是一轮更新中唯一可能的同步点。

> Each agent is fully updated – which means it senses its environment, evaluates its
perceptions by going further through each of its activity graphs and finally performs the scripts
associated with the current activities. The random sequence of updating the agents provides
a reduced form of virtual parallelism: although each agent is fully updated before the next
agent is tackled, the modeler cannot influence the actual sequence of updating the agents.

每个代理都是完全更新的 – 这意味着它会感知其环境，通过进一步浏览其每个活动图来评估其感知，
最后执行与当前活动相关的脚本。更新 Agent 的随机顺序提供了一种简化的虚拟并行形式：
尽管每个 Agent 在处理下一个 Agent 之前都已完全更新，但建模者无法影响更新 Agent 的实际顺序。


#### Agent Update

> There are two sources of dynamics in a multi-agent model: first, the global environment
which is explicitly modeled in SeSAm; second, from the agents with their behavior. As is
noticeable in Figure 16.3, the world can also be seen as an agent, yet with another - more
powerful - behavior repertoire as it may also access information from a global point of view.

多智能体模型中有两个动力学来源：第一，在 SeSAm 中显式建模的全局环境;
第二，来自代理及其行为。如图 16.3 所示，世界也可以被看作是一个代理，
但具有另一个 - 更强大的 - 行为库，因为它也可以从全局的角度访问信息。

> The update sequence of an agent a is the following:
> ```
> For every re in ReasoningEnginges of agent a in given order do
>     repeat until re.currentActivity is of type time-consuming
>         rules ← select rules from re.currentActivity with condition == true
>         if | rules |≥ 1
>             theRule ← getRandom(rules)
>             execute termination sequence of re.currentActivity
>             set re.currentActivity to next activity of theRule
>             execute start sequence of new re.currentActivity
>         execute action sequence of re.currentActivity
> ```
> The update cycle of the world is identical to standard agents. The main difference is that
> the world is allowed to use primitives affecting the complete system.


代理 a 的更新顺序如下：
```
For every re in ReasoningEnginges of agent a in given order do
    repeat until re.currentActivity is of type time-consuming
        rules ← select rules from re.currentActivity with condition == true
        if | rules |≥ 1
            theRule ← getRandom(rules)
            execute termination sequence of re.currentActivity
            set re.currentActivity to next activity of theRule
            execute start sequence of new re.currentActivity
        execute action sequence of re.currentActivity
```
世界的更新周期与标准代理相同。主要区别在于，允许世界使用影响整个系统的基元。


#### Properties of the Update Scheme / 更新方案的属性

> This overall update scheme has advantages and disadvantages. On the one hand its major
advantage lies in its simplicity: the procedure can be easily understood by researchers who
are not experts in distributed systems. No resolution in case of conflicting actions is 
necessary as there is no actual parallelism. On the other side, artefacts — especially when agents
are learning — are prevented by the random update. It is not the case that the exact time
for updating a particular agent is set; the modeler cannot determine the sequence of agent
update.∗

这种整体更新方案有优点也有缺点。一方面，它的主要优点在于其简单性：
非分布式系统专家的研究人员可以很容易地理解该过程。如果 action 发生冲突，则不需要解决，
因为没有实际的并行性。另一方面，手工艺品"artefacts" — 尤其是在代理学习时 — 被随机更新阻止。
更新特定代理程序的确切时间并非如此;建模器无法确定代理 Update 的顺序∗

> Obviously there are critical issues in the update sequence that a modeler must be aware
of: with the randomization of the update sequence comes an additional, potentially hidden
stochastic process that may be responsible for variations in the model output — however,
if exact reproducibility of results is needed, the random seed can be explicitly set in the
initialization of a simulation experiment.

显然，建模者必须注意更新序列中存在关键问题：随着更新序列的随机化，会带来一个额外的、可能隐藏的随机过程，
这可能会导致模型输出的变化——但是，如果需要结果的精确可重复性，可以在模拟实验的初始化中显式设置随机种子。

> Additionally the fact that one agent is updated after the other may result in different
outcomes depending on the actual update sequence. This is important in applications such
as traffic simulation with collision avoiding behavior when an agent may take the position
that was freed by another agent immediately before. Figure 16.5 illustrates this problem by
showing how the update sequence influences the result.

此外，一个代理在另一个代理之后更新这一事实可能会导致不同的结果，具体取决于实际的更新顺序。
这在具有冲突避免行为的交通模拟等应用程序中非常重要，当一个代理可以占据另一个代理之前释放的位置时。
图 16.5 通过显示 update sequence 如何影响结果来说明这个问题。

> These basic problems can be tackled on the model level by dividing one time step into
two virtual ones: one timestep in that every agent is perceiving its environment, reasoning
and the selection of an action. Then the selected actions are executed in a second loop. This
results in the fact that all agents perceive the same situation of the environment, basically
as if they perceive at the same time. We used this emulation of parallelism for simulating
cellular automata using SeSAm. However in our CA case, one agent was only allowed to
manipulate its own status avoiding any conflicts in action performance. If concurrent
modifications of the same environmental entity are possible, then conflict resolution for deciding
which action actually should be taken has to be formulated on the model level ideally in
the behavior definition of the world that is conceptualized as a global entity. Such a model
however becomes very complex.

这些基本问题可以通过将一个时间步长划分为两个虚拟时间步来解决：
一个时间步，因为每个代理都在感知其环境、推理和动作的选择。
然后，在第二个循环中执行所选操作。这导致所有代理都感知到相同的环境情况，基本上就像他们同时感知一样。
我们使用这种并行仿真来模拟使用 SeSAm 的元胞自动机。
然而，在我们的 CA 案例中，一个代理只被允许操纵自己的状态，避免了动作性能中的任何冲突。
如果可以同时修改相同的环境实体，那么决定实际应该采取哪种行动的冲突解决必须在模型级别上制定，
理想情况下是在概念化为全局实体的世界的行为定义中制定。然而，这样的模型变得非常复杂。


### 16.3.3 Plugin Mechanism for Extension / 扩展插件机制

> The language elements described above allow a clear and structured overall model
representation. However it can be quite cumbersome to formulate models just using the
default primitives and structures. Therefore a plugin mechanism was developed that allows
enhancing the language and providing additional supporting tools. In particular a plugin may
contain a set of related functionality consisting of
> 
> - Specific data types, such as a data type path or schedule
> - Feature-level add-ons, like variables added to the simObject class to which it is
    assigned, like a variable that stores the personal schedule.
> - Primitives using the plugin data types, interfaces to plugin variables or simply
    macro-like primitives as support for modeling on a higher level of abstraction
> - Tools providing helpful functionality, like importing spatial information for filling
    situation definitions, etc.
> - Plugins may also come with specific editors or panes.

上述语言元素允许清晰且结构化的整体模型表示。但是，仅使用默认基元和结构来构建模型可能非常麻烦。
因此，开发了一种插件机制，允许增强语言并提供额外的支持工具。具体而言，插件可能包含一组相关功能，包括

- 特定数据类型，例如数据类型路径或计划
- 功能级附加组件，例如添加到其分配到的 simObject 类的变量，例如存储个人日程的变量。
- 使用插件数据类型的基元、插件变量的接口或简单的类似宏的基元，以支持在更高抽象级别上进行建模
- 提供有用功能的工具，例如导入空间信息以填充情况定义等。
- 插件也可能带有特定的编辑器或窗格。

> As mentioned above, prominent plugins are responsible for spatial representations. There
is for example a plugin for 2d worlds adding a map to the world, a spatial information data
type composing position, heading and polygon-based shape representation to simObject
classes. Alternative space representations are 3d maps, graphs connecting node- and edge-
based simObjects, as well as raster and vector GIS-based representations. There are a
variety of additional plugins from primitives that establish connections to data bases to
plugins that allow generating movies from animations.

如上所述，著名的插件负责空间表示。例如，有一个用于 2D 世界的插件，用于向世界添加地图，
一个空间信息数据类型，将位置、航向和基于多边形的形状表示组成到 simObject 类。
替代空间表示包括 3D 地图、连接基于节点和边缘的 simObject 的图形，以及基于 GIS 的栅格和矢量表示。
还有各种其他插件，从建立与数据库连接的基元到允许从动画生成影片的插件。

> The plugin mechanism had been extensively used in SeSAmHospital which can be seen
as a platform for agent-based hospital simulation with a focus on examination scheduling
[Herrler, 2007]. This domain-specific simulator basically consists of SeSAm and a hierarchy
of interrelated plugins providing complex data structures like clinical path representations,
specific patient generation functionality, etc.

插件机制已在 SeSAmHospital 中广泛使用，可以看作是基于代理的医院模拟平台，
重点是检查调度 [Herrler， 2007]。这个特定于领域的模拟器基本上由 SeSAm 和相互关联的插件层次结构组成，
提供复杂的数据结构，如临床路径表示、特定患者生成功能等。

### 16.3.4 Problematic Details of the Language / 语言中有问题的细节

> Working with this language in a variety of simulation projects from simulation of bee
behavior to large shopping behavior models or pedestrian simulations, we discovered that the
language as it is now needs further improvements.

在各种仿真项目中使用这种语言，从蜜蜂行为仿真到大型购物行为模型或行人仿真，我们发现现在的语言需要进一步改进。

> The main critical point is the weak agent interface concept. The modeler may declare
appropriate variables of the agents’ body as “accessible" from outside. A second tag
denotes whether the value of the variable may be manipulated or not. This rudimentary
representation of possible interactions may be apt for implicit interaction; however explicit,
message-based communication needs additional efforts. Thus encapsulation of behavior is
hardly supported by the SeSAm language, but relies on the self-restriction of the modeler.

主要关键点是弱代理接口概念。建模者可以将代理体的适当变量声明为从外部“可访问"。
第二个标签表示是否可以操纵变量的值。这种可能的交互的基本表示可能适合于隐式交互;
无论多么明确，基于消息的通信都需要额外的努力。因此，SeSAm 语言几乎不支持行为的封装，
而是依赖于建模器的自我限制。

> Another missing concept is local, temporary variables that facilitate modularization of
behavioral description by enabling the formulation of intermediate results in computations
within an activity or a user primitive. In the current version of the language, there are
some quite tricky combinations of primitives that allow us to circumvent this restriction –
however such opportunities are just available to SeSAm experts.

另一个缺失的概念是局部临时变量，它通过在活动或用户基元中的计算中支持构建中间结果来促进行为描述的模块化。
在当前版本的语言中，有一些非常棘手的基元组合可以让我们规避这个限制——然而这样的机会只有 SeSAm 专家才能获得。

> A third drawback is the lack of a clear inheritance concept between classes that are
accessible to the modeler. The modeler may just generate a list of instances of the agent
description classes without specifying the relations between instances. Features – as mentioned
before – remedy this problem only marginally as they currently just integrate variables and
user functions. We are currently planning to enhance the features by integrating data types
and partial reasoning engines moving toward a feasible model building block concept.

第三个缺点是建模器可访问的类之间缺少明确的继承概念。建模器可能只生成代理描述类的实例列表，
而不指定实例之间的关系。如前所述，功能只能略微解决这个问题，因为它们目前只是集成变量和用户函数。
我们目前正计划通过集成数据类型和部分推理引擎来增强这些功能，朝着可行的模型构建块概念迈进。


### 16.3.5 General Aspects of Suitability / 适用性的一般方面

> Although it can be shown that the declarative language possesses the power of a general
programming language, one can easily see that it is more apt for modeling a particular kind
of system whereas others might be cumbersome to formulate. In [Kl¨ugl, 2008] three levels
of complexity of architectures for simulated agents were identified: behavior generating that
denotes mainly architectures that use planning from first principles, behavior configuring
architectures, like interpretation and instantiation of skeletal plans and finally behavior
describing architectures, like rule-based behavior descriptions.

尽管可以证明声明性语言具有通用编程语言的强大功能，但人们可以很容易地看到它更适合于对特定类型的系统进行建模，
而其他系统可能难以制定。在 [Kl ̈ugl， 2008] 中，确定了模拟代理架构的三个复杂度级别：
行为生成，主要表示使用主要原则规划的架构，
行为配置架构，如骨骼计划的解释和实例化，
最后是行为描述架构，如基于规则的行为描述。

> In general, SeSAm is particularly apt for simulations involving rather simple agents that
reside in some spatial environment and interact implicitly by manipulating the environment.
Such behavior can be easily formulated using rule-based behavior descriptions. This orig-
inates in the initial applications of SeSAm in the area of social insect simulation. Related
properties can also be found in traffic or pedestrian simulation where successful projects
have been performed. The negotiations formulated for the hospital simulations [Herrler,
2007] show that also message-based interactions can be integrated without any problem
into that frame. They involve the formulation of at least two concurrently active reasoning
engines per agent: one for the actual behavior, one for accepting and interpreting incoming
messages concurrently to the actual behavior. Therefore the overall agent model is slightly
more complex.

一般来说，SeSAm 特别适用于涉及相当简单的代理的模拟，这些代理驻留在某个空间环境中，
并通过操纵环境进行隐式交互。使用基于规则的行为描述可以很容易地表述此类行为。
这在 SeSAm 在社会性昆虫模拟领域的初步应用中起源。在已成功执行项目的交通或行人模拟中也可以找到相关属性。
为医院模拟制定的谈判 [Herrler， 2007] 表明，基于消息的交互也可以毫无问题地集成到该框架中。
它们涉及为每个代理制定至少两个并发活动的推理引擎：一个用于实际行为，
一个用于接受和解释与实际行为同时发生的传入消息。因此，整体代理模型稍微复杂一些。

> In [Rindsf¨user and Kl¨ugl, 2005] we formulated agent behavior as executing and manipu-
lating daily plans stored in state variables of the agents, instead of explicitly and directly
formulating the plan contents in the activity graphs. The model was sufficiently successful
in reproducing travelers’ daily activities, yet the representation and manipulation of such
complex data structures required careful consideration. This is due to the fact that it is not
appropriately supported by the overall system, in terms of providing plan structures and
primitives to modify these plans.

在 [Rindsf ̈user 和 Kl ̈ugl， 2005] 中，我们将代理行为定义为执行和操纵存储在代理状态变量中的日常计划，
而不是在活动图中明确和直接地制定计划内容。该模型在再现旅行者的日常活动方面足够成功，
但这种复杂数据结构的表示和操作需要仔细考虑。这是因为在提供计划结构和原语来修改这些计划方面，
它没有得到整个系统的适当支持。

> SeSAm’s range of applications has widened and experiences with more complex agent
models confirm that formulating more and more complex agent behavior becomes quite
cumbersome. Although a shortest path algorithm can be formulated without any problem
– for example for generating a path as some kind of movement plan in a network – the
integration of real behavior generating approaches is hardly possible. For planning from
first principles, operator descriptions and complex situation descriptions that characterize
goal states must be tackled. As SeSAm does not offer any form of logic-based description of
situations nor any appropriate primitive characterization based on pre- and post-conditions,
such complex architectures are basically impossible.

SeSAm 的应用范围已经扩大，使用更复杂的代理模型的经验证实，制定越来越复杂的代理行为变得相当麻烦。
尽管可以毫无问题地制定最短路径算法 - 例如，在网络中生成路径作为某种运动计划 - 但几乎不可能集成真实的行为生成方法。
对于从第一原则进行规划，必须解决表征目标状态的运算符描述和复杂情况描述。
由于 SeSAm 不提供任何形式的基于逻辑的情况描述，也不提供任何基于前条件和后条件的适当原始特征，
因此这种复杂的架构基本上是不可能的。

## 16.4 Users, Tasks, and SeSAm

> For actually implementing a model using this SeSAm core language, several user interfaces
are supporting different tasks during a simulation study.

为了使用这种 SeSAm 核心语言实际实现模型，在仿真研究期间，多个用户界面支持不同的任务。

> Developing such interfaces within the same visual framework is not an easy task. Much of
the advance of the SeSAm system during the last year is related to these developments. The
following sections will contain a short, sketchy treatment of the different elements of the
overall SeSAm model development and simulation platform offered for the different tasks
mentioned above: visual modeling environment, standard animation, online aggregation and
visualization of key values during simulation, interactive simulation and "agent playing"
environment.

在同一个可视化框架中开发这样的界面并不是一件容易的事。去年 SeSAm 系统的大部分进步都与这些发展有关。
以下部分将包含对整个 SeSAm 模型开发和仿真平台的不同元素的简短粗略处理，这些元素为上述不同任务提供：
可视化建模环境、标准动画、仿真过程中关键值的在线聚合和可视化、交互式仿真和“代理播放”环境。

### 16.4.1 Principles

> As mentioned in the introduction we had several, partially conflicting goals for developing
SeSAm. We wanted to build a system that concurrently enables beginners to implement
their model and that can be used as a fast prototyping tool for experts. Therefore the
system had to fulfill the following general requirements:
> - Hide potential model complexity from beginners
> - Support beginners while learning to implement a model
> - Make all aspects of a model accessible to experts
> - Support experts while implementing a complex, large model

正如引言中提到的，我们开发 SeSAm 有几个部分相互冲突的目标。
我们想构建一个系统，让初学者能够同时实现他们的模型，并且可以用作专家的快速原型设计工具。
因此，系统必须满足以下一般要求：
- 向初学者隐藏潜在的模型复杂性
- 在学习实现模型的同时为初学者提供支持
- 让专家可以访问模型的所有方面
- 在实施复杂的大型模型时为专家提供支持

> Thus for beginners the main issue is simplicity and consistency – for experts it is scalability
of modeling and simulation. In more detail, the following ideas and principles were pursued,
partially motivated by [Green and Petre, 1996] or [Kuljis, 1994].
> 
> - The main difficulty lies in selecting the appropriate primitives: therefore an
    expert may choose to use a different set of primitives than a beginner. The latter
    may use more abstract primitives that encapsulate more functionality than the
    former who may like to completely control every detail and search for the most
    effective implementation of the particular problem at hand. Good examples are
    movement primitives. Whereas the expert may use more basic primitives like
    `changeDirection`, `moveWithSpeed` or `observeObjectsInDirection`, a beginner
    would be happy with a primitive like `moveWhileAvoidingCollisionsWith`...
> - Having learned how to deal with one editor, this experience can be used for all
    editors for similar elements, as GUI interaction remains the same.
> - Including automatic syntax checks or missing opportunities to input something
    syntactically wrong.
> - Functionality as provided by modern software development platforms makes it
    easy to change model design decisions. Examples are refactoring actions or
    navigation means, like searching for references or direct connection to definitions
    of model elements. Also support for model versioning is important for model
    implementation.
> - Documentation facilities should be possible for any element of the model for
    recording why things are formulated as they are. Colors etc. can be used to
    mark model elements where the modeler wants to include more detail. Thus the
    modeler does not have to memorize a lot, but can augment the model with free
    text about his thoughts.
> - Structuring language elements like sub-programs or modules are available in the
    form of user primitives, features or partial situations. Thus modeling becomes
    more scalable for the expert user. Predefined modules support the novice.

因此，对于初学者来说，主要问题是简单性和一致性 - 对于专家来说，是建模和仿真的可扩展性。
更详细地说，遵循以下想法和原则，部分受到 [Green and Petre， 1996] 或 [Kuljis， 1994] 的推动。

- 主要困难在于选择合适的原语：因此，专家可能会选择使用与初学者不同的原语集。
  后者可能使用更抽象的原语，这些原语封装了比前者更多的功能，
  前者可能希望完全控制每个细节并寻找手头特定问题的最有效实现。很好的示例是移动基元。
  虽然专家可能会使用更基本的基元，如 changeDirection、moveWithSpeed 或 observeObjectsInDirection，
  但初学者会对 moveWhileAvoidingCollisionsWith...
- 在学会了如何处理一个编辑器之后，这种体验可以用于类似元素的所有编辑器，因为 GUI 交互保持不变。
- 包括自动语法检查或错过输入语法错误的机会。
- 现代软件开发平台提供的功能使更改模型设计决策变得容易。
  例如，重构操作或导航方式，例如搜索引用或直接连接到模型元素的定义。
  此外，对模型版本控制的支持对于模型实现也很重要。
- 模型的任何元素都应该有文档工具，用于记录事物为何如此表述。
  颜色等可用于标记建模者想要包含更多细节的模型元素。因此，建模者不必记住很多，
  但可以用关于他的想法的自由文本来增强模型。
- 构建语言元素（如子程序或模块）以用户原语、功能或部分情况的形式提供。
  因此，对于专家用户来说，建模变得更加可扩展。预定义的模块支持新手。

### 16.4.2 Developing a Conceptual Model

> This task is not directly supported by SeSAm. One may argue that the high-level model
representations – the classification in agents and resources, the way behavior is characterized
– may support structured thinking about elements of a model. A basic idea of SeSAm is to
bridge the gap between model specification and implementation.

SeSAm 不直接支持此任务。有人可能会争辩说，高级模型表示 – 代理和资源的分类，行为的表征方式 
– 可能支持对模型元素的结构化思考。SeSAm 的一个基本思想是弥合模型规范和实现之间的差距。

### 16.4.3 Visual Programming for Model Implementation

> In our description of the SeSAm system we will first concentrate on the task of model
implementation. Providing a visual programming environment for this task was basically
driven by the idea to make model logics accessible to all interested people, not only model
configuration, model-produced simulation runs or data. Introductory material concerning
visual programming can be found in [Chang, 1990] or more recently in [Lieberman et al.,
2006].

在我们对 SeSAm 系统的描述中，我们将首先专注于模型实现的任务。
为这项任务提供可视化编程环境基本上是由让所有感兴趣的人都可以访问模型逻辑的想法驱动的，
而不仅仅是模型配置、模型生成的仿真运行或数据。
有关视觉编程的介绍性材料可以在 [Chang， 1990] 或最近的 [Lieberman et al.， 2006] 中找到。

> In general one must admit that programming using a well-known textual programming
language in a good environment for development may result in a more efficient modeling
and simulation for the experienced programmer. Even for a person experienced as modeler
using some programming language and class libraries, model implementation supported by
a visual programming environment has many advantages ranging from explainability to
accessibility.

一般来说，我们必须承认，在良好的开发环境中使用众所周知的文本编程语言进行编程可能会为
有经验的程序员带来更高效的建模和模拟。即使对于使用某些编程语言和类库的建模者来说，
可视化编程环境支持的模型实现也具有许多优势，从可解释性到可访问性。

#### Primitive Call Specification / 原始调用规范

> The basic building block of the visual SeSAm programming environment is the specification
of primitives and primitive calls: There is only one way to specify how a primitive is used. It
is used whenever a nested primitive call has to be specified: in the basic behavior description
of activities, in formulating the predicates of rules or user macros, for giving a procedure
to compute initial values, ... to experiment and analysis declaration. This dialog element is
shown in a screenshot in Figure 16.6.
> ![img_38.png](img_38.png)
> FIGURE 16.6 Screenshot of a dialog for specifying primitive calls. This basic dialog element is used
everywhere in the system when this task has to be done. It consists of three parts: the current status of
specification in the left half of the dialog, directly insertable values in the upper right and available primitive
on the right lower half. When clicking on a primitive call, a similar dialog opens resulting in a cascade of
dialogs as indicated by the arrow from one dialog to the other.
> 图 16.6 用于指定原始调用的对话框的屏幕截图。当必须完成此任务时，此基本对话框元素在系统中的任何地方都使用。
> 它由三部分组成： 对话框左半部分的规范当前状态，右上半部分的直接可插入值和右下半部分的可用基元。
> 单击原始调用时，将打开一个类似的对话框，从而产生一系列对话框，如从一个对话框到另一个对话框的箭头所示。

可视化 SeSAm 编程环境的基本构建块是基元和基元调用的规范：只有一种方法可以指定如何使用基元。
每当必须指定嵌套原始调用时，都会使用它：在活动的基本行为描述中，在制定规则或用户宏的谓词时，
用于提供计算初始值的过程，...实验和分析声明。此 dialog 元素如图 16.6 中的屏幕截图所示。

> Using such a basic element, a modeler can completely specify behavior without programming
in a traditional language. The particular procedure for selecting and configuring
reduces syntax error proneness as the user cannot select a primitive that returns a wrong
type. Another element that deals with reducing potential errors is the way in which nested
calls are to be edited. In this case the parent call is no longer accessible for manipulation
which avoids inconsistencies.

使用这样的基本元素，建模者可以完全指定行为，而无需使用传统语言进行编程。
选择和配置的特定过程降低了语法错误的可能性，因为用户无法选择返回错误类型的原语。
处理减少潜在错误的另一个元素是编辑嵌套调用的方式。在这种情况下，父调用不再可用于操作，从而避免了不一致。

> In the right lower corner – mostly hidden in Figure 16.6 – three elements support fast
selection by providing a short cut search item, enlarging the primitive set with “expert-mode
primitives”, like loops or roulette wheel functionality. A small button – the “Edgar” button
in the corner right on the bottom – allows for textual search for appropriate primitive. All
documentation and hints given in the primitive declaration are available there. Edgar also
justifies why certain primitives are not currently available for insertion.

在右下角 - 大部分隐藏在图 16.6 中 - 三个元素支持快速选择，通过提供一个快捷方式搜索项，
用 “专家模式基元” 扩大基元集，如循环或轮盘赌功能。一个小按钮 - 底部角落的 “Edgar” 按钮 - 允许文本搜索合适的原语。
原始声明中给出的所有文档和提示都在那里可用。Edgar 还解释了为什么某些原语当前无法插入。

#### Forms and Tables / 表单和表格

> A typical means for specifying object instances – class declarations as well as agent instances
in the model configuration – are forms where every attribute can be input using appropriate
dialog items [Bamberger et al., 1997]. Forms are used in SeSAm for all fixed meta information
for model elements – for example in specifying a body variable description as visible on the
right side of Figure 16.7.

指定对象实例的典型方法 - 类声明以及模型配置中的代理实例 - 是可以使用适当的对话框项输入每个属性的形式
[Bamberger et al.， 1997]。在 SeSAm 中，表单用于模型元素的所有固定元信息——例如，
在指定 body 变量 description 时，如图 16.7 右侧所示。

> ![img_39.png](img_39.png)
> FIGURE 16.7 Screenshot of a dialog for specifying body variables. This basic dialog element is used
everywhere in the system when language elements that are in a set, have to be specified. This dialog element
has two parts: on the left the list is given, the pane on the right changes with selection of a list element for
enabling the modeler to manipulate the selected element.
> 图 16.7 用于指定主体变量的对话框的屏幕截图。当必须指定集合中的语言元素时，
> 此基本 dialog 元素在系统中的任何地方都使用。此对话框元素包含两个部分：
> 左侧给出了列表，右侧的窗格随着列表元素的选择而变化，以便建模者能够操作所选元素。
> 
> Tables can serve as a more compact representation of object attributes, if the data struc-
tures to represent in one cell are not too complicated. We use tables, for example, to specify
the object instance declarations where the set of object variables that have to be set is not
given, but depends on the class-level declaration.

如果在一个单元格中表示的数据结构不太复杂，则表格可以用作对象属性的更紧凑表示。
例如，我们使用表格来指定对象实例声明，其中没有给出必须设置的对象变量集，而是取决于类级声明。

#### Edit List Elements

> Another structure that is used at many places is depicted in screenshot 16.7. On the left
a list of elements is given; by selecting an item, all information about it is displayed on
the right and can be edited. This dialog form is used for body variables, specification of
simObject instances, analysis items, etc.
> 
> A direct combination of list elements and pure primitive specification can be found on
several occasions. Examples are the list of user functions, the analysis items when instru-
mentation is specified, action sequences in activities, object lists in situations, etc. Once a
modeler has learned how to deal with these modeling elements, this experience is useful all
over SeSAm.

屏幕截图 16.7 中描述了另一种在许多地方使用的结构。
左侧给出了元素列表;通过选择项目，有关该项目的所有信息都显示在右侧，
并且可以进行编辑。此对话框表单用于主体变量、simObject 实例的规范、分析项等。

列表元素和纯原始规范的直接组合可以在多个场合找到。
例如，用户功能列表、指定说明时的分析项、活动中的操作序列、情境中的对象列表等。
一旦建模者学会了如何处理这些建模元素，这种体验在整个 SeSAm 中都很有用。

#### Behavior Specification 

> The primitive specification forms sketched above are used as low-level building blocks for
defining the behavior – basically as atomic statements of the language. The structure of a
reasoning engine or an activity graph is especially apt for visual constructing using some
graph structure. Figure 16.8 shows an example screenshot.
> ![img_40.png](img_40.png)
> FIGURE 16.8 Screenshot of the pane for specifying the behavior description of an agent.
> 
> 图 16.8 用于指定代理行为描述的窗格的屏幕截图。
> 
> There are different node shapes in addition to the previously mentioned start node, end
node or nested activity graphs - for depicting specific properties. These additional shapes
– shown in Figure 16.9 do not result in different forms of treatment in the simulator, but
merely support clarification of functionality for transparency reasons. Exceptions are the
documentation nodes which are ignored. Only one look at the behavior describing graph
is necessary to identify decision, sensing activities, etc. For additional overview, different
colorings of activities are available. For a short look at the activity contents the beginning of
the action primitive calls are also depicted using a small text size – see activities in Figure
16.8.
> ![img_41.png](img_41.png)
> FIGURE 16.9 Different shapes of activity nodes in reasoning engine modeling. Only composed activity
nodes – which hide a new activity graph – bear special semantics for interpretation. Documentation nodes
(the most right ones) are ignored for behavior generation. The others only serve for enable the modeler to
oversee a complex graph.
> 
> 图 16.9 推理引擎建模中不同形状的活动节点。只有组合的活动节点（隐藏新的活动图）才具有用于解释的特殊语义。
> 文档节点（最右边的）在行为生成时被忽略。其他的仅用于使建模者能够监督复杂的图形。
> 
> Edges in the activity graph editor denote rules for terminating their predecessor and ini-
tiating their successor activity. The subtitles of these edges are generated from the primitive
combination that forms the condition of the rules. These generated texts can however be
replaced by the modeler. Thus the modeler has several options for implementing a well-
structured and clearly structured activity graph.

上面草拟的基元规范形式被用作定义行为的低级构建块 —— 基本上是语言的原子语句。
推理引擎或活动图的结构特别适合使用某些图形结构进行可视化构建。图 16.8 显示了一个示例屏幕截图。

除了前面提到的开始节点、结束节点或嵌套活动图之外，还有不同的节点形状 - 用于描述特定属性。
这些额外的形状 – 如图 16.9 所示，在模拟器中不会导致不同形式的处理，而只是出于透明原因支持功能澄清。
例外情况是被忽略的文档节点。只需看一眼行为描述图即可识别决策、感知活动等。
有关其他概述，可以使用不同颜色的活动。为了简要地了解活动内容，
动作原语调用的开头也使用较小的文本大小来描述 - 参见图 16.8 中的活动。

活动图编辑器中的边表示终止其前置活动并启动其后续活动的规则。
这些边缘的子标题是从构成规则条件的原始组合生成的。但是，这些生成的文本可以由建模器替换。
因此，建模者有多种选择来实现结构良好且结构清晰的活动图。

#### Configuration of Start Situations
> Without additional plugins the start situation merely consists of the description of one
world instance and of a set of agent and resource class instances. This is done using already
known lists and tables.

如果没有额外的插件，启动情况仅包括一个世界实例和一组代理和资源类实例的描述。这是使用已知的列表和表格完成的。
 
> Additionally editors coming with one of the spatial plugins play a particular role, as they
allow positioning on maps using drag and drop functionality.

此外，其中一个空间插件附带的编辑器也发挥着特殊的作用，因为它们允许使用拖放功能在地图上进行定位。

#### Accessibility and Documentation  辅助功能和文档

> Two important issues in a visual programming system are navigation and documentation.
One prerequisite for useful development environments for programming is the way to find the
elements that the user wants to edit. The user should not be required to memorize names,
but to have directly at hand all necessary information for manipulating an element. For
example, when formulating an agent’s behavior, variables of the agent should be accessible
with one click when they are missing or are set to the wrong data type. Also the user
should not need to memorize the exact functionality of a user function, but should be able
to immediately access it.

可视化编程系统中的两个重要问题是导航和文档。有用的编程开发环境的一个先决条件是找到用户想要编辑的元素的方法。
不应要求用户记住名称，而是直接掌握操作元素所需的所有信息。例如，在制定代理的行为时，
如果代理的变量缺失或设置为错误的数据类型，则只需单击一下即可访问这些变量。
此外，用户不需要记住用户函数的确切功能，但应该能够立即访问它。

> In SeSAm tool tips can be edited directly by the modeler for augmenting the documen-
tation of the model. A right click always leads to a context menu where related elements of
the definition are accessible. Every element – from user primitive to status variable to ac-
tivities – can be given additional, explanatory text. These modeling GUI elements increase
scalability of the implementation which is particularly important for complex multi-agent
simulation models.

在 SeSAm 中，建模者可以直接编辑工具提示，以增强模型的文档。
右键单击始终指向一个上下文菜单，可在其中访问定义的相关元素。
每个元素 - 从用户基元到状态变量再到活动 - 都可以被赋予额外的解释性文本。
这些建模 GUI 元素提高了实现的可扩展性，这对于复杂的多智能体仿真模型尤为重要。

### 16.4.4 Experiment Scripting and DAVINCI for Experimenters / 实验脚本和实验人员的 DAVINCI

> The second task that has to be executed during a simulation study is extensive experimentation.
It is basically done for model testing and – after the necessary model quality has
been guaranteed – for making the actual deployment runs generating the intended results.
Whereas programming and formalization expertise can be seen as a prerequisite for users
fulfilling the role of a modeler, pure experimentation contains a lot of rather simple
operations with several repetitions – if the configuration to be run is known. The main intelligence
in the experimentation task however has to be used for an intelligent design of experiments
as well as for analyzing the output data in order to initiate additional simulation runs.

在仿真研究期间必须执行的第二项任务是广泛的实验。它基本上是为了模型测试而完成的，
并且在保证必要的模型质量之后，用于使实际部署运行产生预期的结果。
虽然编程和形式化专业知识可以被视为用户履行建模者角色的先决条件，
但纯粹的实验包含许多相当简单的操作，并且需要多次重复 - 如果要运行的配置是已知的。
然而，实验任务中的主要智能必须用于实验的智能设计以及分析输出数据，以便启动额外的模拟运行。

> It is absolutely unacceptable to trigger all necessary simulation runs manually. Therefore
the configuration of experiment scripts is or at least should be part of every modeling and
simulation framework. In SeSAm there are two ways of defining and controlling simulation
experimentation: the first consists of basically a script using additional primitives that
operate on situation configurations, simulation run definitions. These primitives may set
the random seed for ensuring exact reproducibility of results or may initiate runs based
on systematic parameter variations. As the user interface is similar to all primitive call
specification dialogs, the original modeler can easily input such experimentation scripts.

手动触发所有必要的仿真运行是绝对不可接受的。因此，实验脚本的配置是或至少应该是每个建模和仿真框架的一部分。
在 SeSAm 中，有两种定义和控制仿真实验的方法：第一种基本上由一个脚本组成，该脚本使用额外的基元来操作情况配置、
仿真运行定义。这些基元可以设置随机种子以确保结果的精确可重复性，或者可以根据系统参数变化启动运行。
由于用户界面与所有基元调用规范对话框类似，因此原始建模者可以轻松输入此类实验脚本。

> The second possibility was developed for supporting calibration in the PhD thesis of M.
Fehler [Fehler, 2008 or 2009]. Besides other methodological advances, he developed a tool
named DAVINCI that allows automatic parameter optimization for adjusting the model for
maximizing a model-specific function that expresses some degree of validity of the current
simulation configuration. Information about concepts and technologies behind the tool can
be found in [Fehler et al., 2006] or [Fehler et al., 2005]. DAVINCI can be used more generally
for systematic parameter screening as well as for all kinds of optimization based on methods
ranging from tabu search to genetic algorithms. Therefore it forms a highly valuable tool
for an experimenter. Due to the conceptual complexity for configuring all elements of the
optimization algorithms, such as input parameter, evaluation function, parameter of the
optimization, and parameter of the result presentation, this tool is implemented like a
wizard that guides the user through complex configurations.

第二种可能性是为支持 M. Fehler 的博士论文 [Fehler， 2008 或 2009] 中的校准而开发的。
除了其他方法上的进步外，他还开发了一个名为 DAVINCI 的工具，该工具允许自动优化参数以调整模型，
以最大化模型特定功能，从而表达当前仿真配置的一定程度的有效性。有关该工具背后的概念和技术的信息，
请参见 [Fehler et al.， 2006] 或 [Fehler et al.， 2005]。DAVINCI 可以更普遍地用于系统
参数筛选以及基于从禁忌搜索到遗传算法的各种方法的优化。因此，它为实验者提供了非常有价值的工具。
由于配置优化算法的所有元素（例如输入参数、评估函数、优化参数和结果表示参数）的概念复杂性，
因此该工具的实现类似于向导，可指导用户完成复杂的配置。

### 16.4.5 Online Aggregated Data Presentation and Animation / 在线聚合数据演示和动画

> Another functionality that is primarily used for testing and analyzing the model dynamics
is the animation facility and the online visualization of aggregated data during a simulation
run. These techniques for observing what is happening during a simulation can be seen as a
standard for simulation environments. Basically every user of the simulation models wants
to observe animations.

另一个主要用于测试和分析模型动力学的功能是动画设施和仿真运行期间聚合数据的在线可视化。
这些用于观察模拟过程中发生的情况的技术可以被视为模拟环境的标准。
基本上，仿真模型的每个用户都希望观察动画。

> When the animation is enabled all changes are shown immediately when they happen. If
the standard 2d plugin is used, the behavior may be enriched using primitives for updating
the visualization of an agent, for example by changing the image for its graphical represen-
tation, its color or intentionally draw lines or circles into the map pane for visualizing paths
that the agent has followed, etc. Figure 16.10 shows a small part of the animation view of
a Pedestrian simulation of the SBB Bern Railway Station [Rindsf¨user and Kl¨ugl, 2007].
> ![img_42.png](img_42.png)
> FIGURE 16.10 A part of an animation window showing agents with different attributes (colors) and
their paths. 
> 
> 图 16.10 动画窗口的一部分，显示具有不同属性（颜色）的代理及其路径

启用动画后，所有更改都会在发生时立即显示。如果使用标准的 2D 插件，则可以使用基元来丰富行为，
以更新代理的可视化，例如通过更改图像的图形表示、颜色或有意在地图窗格中绘制线条或圆圈以可视化代理所遵循的路径等。
图 16.10 显示了 SBB 伯尔尼火车站行人模拟的一小部分动画视图 [Rindsf ̈用户和 Kl ̈ugl，2007 年]。

> As the speed of a simulation run may be too slow for reasonable observation, a recording
plugin has been developed that allows one to save animations as movie files for later analysis.
The results of the primitive calls for collecting output data from simulation run can be
written into a file for later analysis – which is actually done during model deployment. For
testing, the same data can be shown directly after generating, using either a series chart or
using a block chart, depending on the volume and dynamics of the data. In Figure 16.11
the relation between analysis definition and curve is shown.
> ![img_43.png](img_43.png)
> FIGURE 16.11 Based on the function specification for output function, aggregated data is shown.  
> 
> 图 16.11 根据 output 函数的函数规格，显示聚合数据。

由于模拟运行的速度可能太慢而无法进行合理观察，因此开发了一个录制插件，允许将动画保存为电影文件以供以后分析。
用于从仿真运行中收集输出数据的基元调用结果可以写入文件以供以后分析，这实际上是在模型部署期间完成的。
对于测试，可以使用系列图或块状图在生成后直接显示相同的数据，具体取决于数据的数量和动态。
在图 16.11 中显示了分析定义和曲线之间的关系。

> There is a small enhancement that makes the animation even more valuable: a debugger.
If a simulation reaches a predefined point in its behavior definition, it stops and the agent
that caused the break can be analyzed more deeply. A stepper functionality allows action-
by-action advancement of the simulation execution. Also, debugger and stepper belong to
the equipment of standard programming environments and thus should be also available for
testing simulation models.

有一个小的增强功能使动画更有价值：调试器。如果模拟达到其行为定义中的预定义点，它将停止，
并且可以更深入地分析导致中断的代理。步进功能允许逐个动作推进仿真执行。
此外，调试器和步进器属于标准编程环境的设备，因此也应该可用于测试仿真模型。

### 16.4.6 Model-Specific Interfaces

> The previous tasks required direct and extensive understanding of the implementation of
the model. A user that is not involved into implementation and testing of a model, but
wants to observe its dynamics, needs a model-specific user interface for “playing around”
with the model. Interaction with the model may take two forms: either as an experimenter
or observer from outside or alternatively from inside the running simulation. The outside
view is basically standard: a human observes the dynamics of the model from outside and
manipulates global parameters or sets local switches in reaction to the observation. The
inside view is particular for agent-based simulation and is often referred to as participatory
simulations (see [Guyot and Honiden, 2006]). In this case a human is controlling one agent,
perceiving what the agent may perceive and manipulating the simulation through the agent’s
effectors. SeSAm supports both forms of interaction. We first tackle specific model interfaces
followed by participatory simulation in the next subsection.

前面的任务需要对模型的实现有直接和广泛的了解。不参与模型的实现和测试，但想要观察其动态的用户，
需要一个特定于模型的用户界面来“玩转”模型。与模型的交互可以采取两种形式：作为外部的实验者或观察者，
或者从正在运行的模拟内部。外部视图基本上是标准的：人类从外部观察模型的动态，
并操纵全局参数或设置局部开关以响应观察结果。内部视图特别适用于基于代理的模拟，
通常被称为参与式模拟（参见 [Guyot 和 Honiden，2006 年]）。在这种情况下，人类控制一个代理，
感知代理可能感知的内容，并通过代理的效应器操纵模拟。SeSAm 支持两种形式的交互。
我们首先处理特定的模型接口，然后在下一小节中进行参与式仿真。

> In order to provide functionality of interfaces for observing and controling simulation runs
in a user-adapted way, we enhanced SeSAm with a graphical GUI builder. We assume that
this element of SeSAm is actually used by the modeler for providing specific interfaces for
more or less experienced people using or testing the model. Examples for addressees may
be stakeholders, but it is also apt for publishing demo versions of a model. Concerning its
functionality, such a model-specific simulation interface corresponds to the type of model
interface that a user may know from other simulation tools.

为了提供以用户适应的方式观察和控制仿真运行的界面功能，我们使用图形 GUI 构建器增强了 SeSAm。
我们假设 SeSAm 的这个元素实际上被建模者用于为或多或少有经验的使用或测试模型的人提供特定的接口。
收件人的示例可能是利益相关者，但它也适用于发布模型的演示版本。就其功能而言，
这种特定于模型的仿真接口对应于用户可能从其他仿真工具中了解的模型接口类型。

> The construction of a simulation specific user interface is done in two phases. At first the
modeler determines the interfaces of the model elements - for example he specifies that the
variable “storage” is manipulatable by the user and then arranges the pre-defined items to
an overall user interface. Figure 16.12 shows a screenshot of the visual GUI builder together
with an instance of the specific user interface.
>![img_44.png](img_44.png)
> FIGURE 16.12 A model-specific interface to a simulation run is generated based on an interface configuration.
> 
> 图 16.12 根据接口配置生成仿真运行的特定模型接口。

仿真特定用户界面的构建分两个阶段完成。首先，建模者确定模型元素的接口 - 例如，
他指定变量 “storage” 可由用户操作，然后将预定义的项目安排到整个用户界面中。
图 16.12 显示了可视化 GUI 构建器的屏幕截图以及特定用户界面的实例。

### 16.4.7 Agent Playing for Advanced Participation / 代理人参与高级参与

> Another development regarding SeSAm interfaces and user task is the so-called “agent
playing” framework (see [Raupach, 2007]). It basically forms the logical advancement of
the interactive simulation runs described in the last subsection. There a bird’s eye view is
used for monitoring the model dynamics from the outside. Agent-based simulation allows
an inside view when a human is playing one particular agent.

关于 SeSAm 接口和用户任务的另一种发展是所谓的“代理播放”框架（参见 [Raupach， 2007]）。
它基本上构成了上一小节中描述的交互式模拟运行的逻辑进展。那里的鸟瞰图用于从外部监控模型动态。
基于代理的模拟允许在人类扮演一个特定代理时获得内部视图。

> This interactive element was developed not for allowing simulation games, but especially
for supporting plausibility testing and validation on the agent level: we assume that for
qualitative validation purposes, the modeler needs to perceive the simulated environment
through the eyes of the agent, immersed into the simulation. While perceiving what the con-
trolled agent perceives and evaluating its reactions to perceptions, as well as while observing
the other agents, a human may evaluate whether the observed simulation run actually is
plausible.

开发此交互式元素不是为了允许模拟游戏，而是为了支持代理级别的合理性测试和验证：
我们假设出于定性验证目的，建模者需要通过代理的眼睛感知模拟环境，沉浸在模拟中。
在感知被控主体感知到的东西并评估其对感知的反应时，以及在观察其他主体时，
人类可以评估观察到的模拟运行是否真的合理。

> The “agent playing” framework consists of two parts: enhancements on the SeSAm side
and a specialized piece of software that visualizes the perceptions of the agent and its actions
outside of SeSAm:
> - SeSAm models have to be enhanced with primitive calls sending and requesting
    all information marked as necessary.
> - An additional program has to be developed that receives the information from
    SeSAm and visualizes this information appropriately. This program may also
    interpolate between two sets of information – for example, visualizing a smooth
    movement in a discrete world. It may be used for mere observation, but also for
    controlling the agents by collecting the commands from the user and thus forcing
    the agent to do what the human wants the agent to do.

“代理播放”框架由两部分组成：SeSAm 端的增强功能和可视化代理的感知及其在 SeSAm 之外的操作的专用软件：

- SeSAm 模型必须通过原始调用来增强，发送和请求所有标记为必要的信息。
- 必须开发一个额外的程序来接收来自 SeSAm 的信息并适当地可视化这些信息。
  该程序还可以在两组信息之间进行插值 - 例如，在离散世界中可视化平滑运动。
  它可以用于单纯的观察，也可以用于通过收集用户的命令来控制代理，
  从而迫使代理做人类希望代理做的事情。

> Thus “agent playing” supports conceptual validation of an agent’s behavior, as the experts
of the original system can adopt the perspective of the agent. Hopefully they can see the
simulated surroundings of the agent from the same perspective as in real life - resulting in
more direct, immersive testing by a human expert.

因此，“代理播放”支持对代理行为的概念验证，因为原始系统的专家可以采用代理的视角。
希望他们能够从与现实生活中相同的角度看到代理的模拟环境，从而由人类专家进行更直接、更身临其境的测试。

## 16.5 Experiences

> Besides use in teaching, SeSAm was and is applied in several simulation projects reaching
from simulation of social insects, reproduction of shopping behavior to agent-based traffic
simulation. Beyond such traditional application areas of agent-based simulation, SeSAm
forms the technical base for virtual high bay warehouses that are used for software tests,
requirements engineering or employee training. In several of these projects, domain experts
like biologists, geographers, etc. use SeSAm independently. In other projects we use the tool
ourselves. The latter allows evaluating usability directly by ourselves.

除了用于教学外，SeSAm 还应用于多个模拟项目，从社交昆虫的模拟、购物行为的再现到基于代理的交通模拟。
除了基于智能体的仿真的传统应用领域之外，SeSAm 还构成了用于软件测试、需求工程或员工培训的虚拟高架仓库的技术基础。
在其中一些项目中，生物学家、地理学家等领域专家独立使用 SeSAm。在其他项目中，我们自己使用该工具。
后者允许我们自己直接评估可用性。

> We can identify three classes of users of SeSAm who are all at least trying to execute
all tasks listed in Section 16.2.1. First of all there are absolute beginners, for example do-
main experts who discover simulation as a scientific tool but never or hardly have used
this methodology and these techniques before. Secondly one may identify a user group
that has experiences in formalization of software of programs without being familiar to the
multi-agent system paradigm. The third class of users are those familiar with the modeling
paradigm, with programming languages as well as with the features of the SeSAm language
and system. We will shortly discuss what we observed with the first two user classes, followed
by some general aspects. It is quite obvious that this cannot replace a systematic evalua-
tion, but may give indications about the feasibility of using SeSAm for doing multi-agent
simulations beyond mere stability and simulation speed.

我们可以识别出三类 SeSAm 用户，他们至少都在尝试执行 Section 16.2.1 中列出的所有任务。
首先是绝对的初学者，例如主要专家，他们发现仿真是一种科学工具，但以前从未或几乎没有使用过这种方法和这些技术。
其次，人们可能会识别出一个用户组，该用户组具有程序软件正规化的经验，但不熟悉多代理系统范式。
第三类用户是熟悉建模范式、编程语言以及 SeSAm 语言和系统功能的用户。
我们稍后将讨论我们在前两个 user 类中观察到的情况，然后是一些一般方面。
很明显，这不能取代系统评估，但可能会表明使用 SeSAm 进行多智能体模拟的可行性，而不仅仅是稳定性和模拟速度。

### 16.5.1 Novices / 新手

> In particular, modeling and implementation novices were one of the premier addressees
that SeSAm was developed for. In general one must admit that SeSAm is too complex for
beginners, although the basic language with variables capturing the status of the entities,
the activity graphs based description was accepted quite easily.

> Modeling and simulation novices with a minimum of formalization training were quite
successful. As experts in biology, geography or economic processes, they were not familiar
with particular programming languages, but had a quite clear image of the agent-based
model that they wanted to develop before starting with SeSAm. Abstraction in general
was not a problem. Their minimum training consisted of programming courses in school
or early university studies. Although they could not practically use the learned programming 
language any more, basic concepts of implementation were still present. Their major
difficulty in implementation consisted of finding and selecting the appropriate primitive
from the large set of atomic functions. As they knew rather exactly what they wanted to
model, they had no conceptual problem and needed only episodic hints how to formulate
exactly certain aspects. It was basically this user group that requested additional support
for experimentation, sensitivity analysis, calibration and validation.

> Another novice user group without any remarkable training in abstraction and formalization
believed the promise of accessibility of agent-based simulation using SeSAm and
addressed us for support. They also came with a model in mind that, however, was too
vague to be implementable independent from a particular tool. Support was not restricted
to how to formulate certain aspects in SeSAm, but started with a more general discussion
about implementation of models that involves both abstraction and concretization. At
least in three to four cases, the modeler was individually “mentored” by a computer
science student who usually also implemented the model to a large extent. The advantage of
SeSAm here was that the model always remained understandable for the domain modeler
although he or she was not able to produce the model itself actively. Although the
modeling novice was merely passive and needed a lot of support, the simulation project itself
could be successfully terminated as long as the student abstained from biasing the model
implementation, but thoroughly attended to the aspects that the domain modeler actually
wanted to express.

> It has been argued that especially the latter user group could be supported by providing
a more powerful primitive set. By using abstract building blocks, a first model could be
constructed. When the un-experienced modeler wonders about how certain outcomes were
produced, the high-level primitives are questioned and replaced by primitive combinations
that the user itself controlled. The advantage would be that the initial gap when formulating
a working model is reduced. The idea of building blocks and component-based simulation
is nothing new, see for example [Barros et al., 2004] or [Valentin et al., 2003], but may also
be useful in the context of SeSAm.

特别是，建模和实现新手是 SeSAm 开发的主要对象之一。一般来说，必须承认 SeSAm 对于初学者来说太复杂了，
尽管带有变量的基本语言捕获实体的状态，基于活动图的描述很容易被接受。

建模和仿真新手，经过最低限度的正规化培训，相当成功。作为生物学、地理学或经济过程方面的专家，
他们不熟悉特定的编程语言，但在开始使用 SeSAm 之前，他们对想要开发的基于代理的模型有相当清晰的印象。
抽象通常不是一个问题。他们的最低培训包括学校或早期大学学习的编程课程。尽管他们无法再实际使用所学的编程语言，
但实现的基本概念仍然存在。它们在实现方面的主要困难在于从大量原子函数中查找和选择合适的原语。
由于他们非常确切地知道他们想要建模什么，因此他们没有概念问题，只需要如何准确构建某些方面的情节提示。
基本上，正是这个用户组要求为实验、灵敏度分析、校准和验证提供额外支持。

另一个没有接受过任何抽象和形式化培训的新手用户组相信使用 SeSAm 进行基于智能体的仿真的可访问性，
并向我们寻求支持。他们还考虑了一个模型，但是，该模型过于模糊，无法独立于特定工具实现。
支持不仅限于如何在 SeSAm 中制定某些方面，而是从关于涉及抽象和具体化的模型实现的更一般性讨论开始。
至少在三到四种情况下，建模者由计算机科学学生单独“指导”，该学生通常也在很大程度上实施了模型。
SeSAm 的优势在于，尽管领域建模者无法主动生成模型本身，但他或她始终可以理解模型。
尽管建模新手只是被动的，需要大量的支持，但只要学生不偏向模型实现，而是彻底关注领域建模者真正想要表达的方面，
仿真项目本身就可以成功终止。

有人认为，特别是后一个用户组可以通过提供更强大的原始集来支持。通过使用抽象构建块，可以构建第一个模型。
当没有经验的建模者想知道某些结果是如何产生的时，高级基元会受到质疑，并被用户自己控制的基元组合所取代。
优点是在制定工作模型时的初始差距会减少。构建块和基于组件的仿真的想法并不是什么新鲜事，
例如 [Barros et al.， 2004] 或 [Valentin et al.， 2003]，但在 SeSAm 的上下文中也可能有用。

### 16.5.2 Knowledgeable in Implementation, Not in Multi-Agent systems / 了解实施，而不是多代理系统

> Basically, this group of SeSAm users consisted of computer science students attending a
course on multi-agent systems. They had two problems. First, lack of documentation
beyond simple tutorials. This information basically confused them as they had certain
expectations about the platform, but could not identify used concepts. A good example is a
student that created one class for every agent to be used in the situation mixing classes
and instances. Several other students had problems in understanding that activity graphs
denote the complete behavior and are not passed completely once per update cycle.

> Another problem was that in general too much functionality was performed by the global
world entity that should have assigned to the agents. The SeSAm language does not enforce
an agent-oriented implementation. Thus, it is possible to let the global entity loop through
all agents and manipulate their status from this central perspective. The students in the
Multi-Agent Systems course had problems abandoning the known process-oriented way of
thinking and replacing it with some interaction-oriented approach, especially when they use
a graph-based language that is similar to process declarations. A missing clear separation
of responsibilities of global environmental model and local agent model is a drawback of
SeSAm for this user group.

基本上，这组 SeSAm 用户由参加多代理系统课程的计算机科学学生组成。
他们有两个问题。首先，除了简单的教程之外，缺乏文档。这些信息基本上让他们感到困惑，
因为他们对平台有一定的期望，但无法识别使用的概念。一个很好的例子是，一个学生为每个代理创建了一个类，
用于混合类和实例的情况。其他几名学生在理解活动图表示完整行为而不是在每个更新周期中完全传递一次时遇到了问题。

另一个问题是，通常，本应分配给代理的 global world 实体执行了太多功能。
SeSAm 语言不强制实施面向代理的实现。因此，可以让全局实体遍历所有代理并从这个中心视角操纵它们的状态。
多智能体系统课程的学生在放弃已知的面向流程的思维方式并用一些面向交互的方法取而代之时遇到了问题，
尤其是当他们使用类似于流程声明的基于图形的语言时。缺少全局环境模型和本地代理模型的明确职责分离是 
SeSAm 对该用户组的缺点。


## 16.6 General Discussion and Future Work

> We believe that with SeSAm an important step was taken toward the advance of simulation
environments for agent-based models, despite of all its drawbacks. Coupling visual programming
and simulation makes the agent-based simulation paradigm accessible for a variety of
modelers that would otherwise not be able or willing to deal with agent-based simulations,
as bridging the gap between a standard programming language and their model concept
would be too demanding for them.

> Nevertheless, there are some starting points for future improvements. Clearly, the simulation
performance of SeSAm should be better. The simulator of SeSAm interprets a behavior
representation that is compiled from the high-level model description given by the modeler.
During this compiling step, optimization steps from compiler design are applied. A simulation
run within the SeSAm framework, however, cannot be as fast as a corresponding direct
implementation without the SeSAm overhead for example using Java. Clearly, one can also
implement efficiently using the SeSAm high-level language based on some coarse knowledge
of lower level primitive implementation which results in reasonable, yet not optimal,
simulation run times. For testing alternative ways, we already experimented with a tool that
generates plain Java code out of a SeSAm model [Niederle, 2005]. This tool worked for very
simple models; however for applying it to more complex models, many generic possibilities
of SeSAm would have to be re-implemented in that compiler tool causing a tremendous
development effort with doubtable success. Thus, the starting point for increasing simulation
speed should be the reduction of overhead by decoupling modeling and runtime environment
in a more consequent way than done in SeSAm up to now. Additionally, the implementation
of certain primitives, especially concerning spatial perception, must be improved.

> There are some additional aspects that are seen as suboptimal. Modelers have to get
used to the prefix notation of primitive calls that is one of the remainders of the original
Lisp-based system. Another aspect that needed explanation in several cases is the separation
between class and instance description. Modelers would intuitively like to start with
(example) configurations, especially when spatially explicit models are to be developed.
SeSAm however biasses the modeler to start with the basic structures instead of starting
by arranging entities on a map.

> These aspects can be remedied or avoided with sufficient training (and sufficient
documentation). This alone however cannot enable a user to develop a successful simulation study
as SeSAm only covers the implementation, experimentation and analysis of an agent-based
simulation. The first step is model design. The step after implementation mainly consists
of testing for validity. These two phases are essential. If one of them fails, the simulation
study fails all together. It is completely justified that such general methodological aspects
gain more and more attention, like in [Matteo et al., 2006]. There are two more visionary
directions that we want to pursue in our future work. We want to investigate new ways of
modeling for circumventing the design problem and secondly, provide more methodological
support for all phases in an agent-based simulation study.

>Up to now, when dealing with end user programming, we just considered approaches
based on visual programming. Research in this direction also proposes learning by
demonstration as a means for implementing agents directly by users. We want to test these forms
of supervised learning and also other forms of learning and adaptive agents for supporting
the development of agent-based models beyond mere implementation and analysis. We are
performing first experiments with agents controlled by neural networks and by machine
learning algorithms. The main problem is defining the appropriate perceptions and
feedback functions that the agents may get from the environment for actually determining the
direction of adaptation. In these learning agents’ applications, we are not aiming at
reproducing, for example, evolutionary processes, but trying to develop a tool that, for example,
automatically generates the behavior of a simulated pedestrian instead of leaving the user
with the cumbersome trial-and-error procedure for model design finding out which rules are
the most appropriate.

我们相信，尽管 SeSAm 存在所有缺点，但 SeSAm 还是朝着基于智能体的模型的仿真环境的发展迈出了重要的一步。
将可视化编程和仿真相结合，使各种建模者可以使用基于智能体的仿真范式，否则这些建模者将无法或不愿意处理
基于智能体的仿真，因为弥合标准编程语言与其模型概念之间的差距对他们来说要求太高了。

尽管如此，未来仍有一些改进的起点。显然，SeSAm 的仿真性能应该更好。SeSAm 的模拟器解释从建模者给出的
高级模型描述编译的行为表示。在此编译步骤中，将应用编译器 design 中的优化步骤。但是，如果没有 SeSAm 
开销（例如使用 Java），在 SeSAm 框架中运行的仿真速度无法与相应的直接实现一样快。
显然，也可以基于对较低级别 primitive implementation 的一些粗略知识，使用 SeSAm 高级语言有效地实现，
从而产生合理但不是最佳的仿真运行时间。为了测试替代方法，我们已经试验了一种从 SeSAm 模型生成纯 Java 
代码的工具 [Niederle， 2005]。这个工具适用于非常简单的模型;然而，要将其应用于更复杂的模型，SeSAm 
的许多通用可能性必须在该编译器工具中重新实现，这会导致巨大的开发工作，但成功值得怀疑。
因此，提高仿真速度的起点应该是通过以比目前在 SeSAm 中更后续的方式解耦建模和运行时环境来减少开销。
此外，必须改进某些基元的实现，尤其是关于空间感知的实现。

还有一些其他方面被视为次优。建模者必须习惯原始调用的前缀表示法，这是原始基于 Lisp 的系统的其余部分之一。
在一些情况下需要解释的另一个方面是类和实例描述之间的分离。建模者直观地希望从 （示例） 配置开始，
尤其是在要开发空间显式模型时。然而，SeSAm 使建模者偏向于从基本结构开始，而不是从在地图上排列实体开始。

这些方面可以通过足够的培训（和足够的文档）来补救或避免。然而，仅凭这一点并不能使用户能够开发成功的仿真研究，
因为 SeSAm 仅涵盖基于智能体的仿真的实现、实验和分析。第一步是模型设计。实施后的步骤主要包括有效性测试。
这两个阶段是必不可少的。如果其中一个失败，则仿真研究将一起失败。完全有理由认为，
这种一般的方法论方面得到了越来越多的关注，就像 [Matteo et al.， 2006] 一样。
在未来的工作中，我们还希望追求两个更有远见的方向。我们希望研究新的建模方法来规避设计问题，
其次，为基于智能体的仿真研究的所有阶段提供更多的方法支持。

到目前为止，在处理最终用户编程时，我们只考虑基于可视化编程的方法。这个方向的研究还提出了
通过演示学习作为用户直接实现代理的一种手段。我们希望测试这些形式的监督学习以及其他形式的学习和自适应代理，
以支持基于代理的模型的开发，而不仅仅是实现和分析。我们正在使用由神经网络和机器学习算法控制的代理进行首次实验。
主要问题是定义代理可能从环境中获得的适当感知和反馈功能，以实际确定适应的方向。
在这些学习代理的应用程序中，我们的目标不是复制进化过程，而是尝试开发一种工具，
例如，自动生成模拟行人的行为，而不是让用户使用繁琐的试错程序进行模型设计，找出哪些规则最合适。


## Acknowledgment

> Many people have contributed to create a platform like SeSAm: Christoph Oechslein was
responsible for the basic implementation of Java-based version. Rainer Herrler technically
supervised the developments during the last years. Manuel Fehler took care about the
experimentation framework. Cornelia Triebig currently deals with reusability and Reinhard
Hatko analyzes the use of adaptive agents. Generations of students have also contributed
to SeSAm.

许多人为创建像 SeSAm 这样的平台做出了贡献：Christoph Oechslein 负责基于 Java 的版本的基本实现。
Rainer Herrler 在过去几年中对开发项目进行了技术监督。Manuel Fehler 负责实验框架。
Cornelia Triebig 目前负责研究可重用性，Reinhard Hatko 分析了适应性代理的使用。
一代又一代的学生也为 SeSAm 做出了贡献。

