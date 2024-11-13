# MAS for Simulation

> 9 Challenges of Country Modeling with Databases, Newsfeeds, and Expert Surveys

> 10 Crowd Behavior Modeling: From Cellular Automata to Multi-Agent Systems

> 11 Agents for Traffic Simulation

> 12 An Agent-Based Generic Framework for Symbiotic Simulation Systems

> 13 Agent-Based Modeling of Stem Cells


- 9 使用数据库、新闻源和专家系统建模的挑战
- 10 人群行为建模：从元胞自动机到多智能体系统
- 11 个用于交通模拟的代理
- 12 基于智能体的共生仿真系统通用框架
- 13 基于代理的干细胞建模


> Multi-agent systems are used as a metaphor in modeling and simulation. At the level
of modeling it supports a view of the system under study as a community of interacting
autonomous entities. At the level of simulation it helps the design of simulation systems as
distributed concurrent entities that interact with their physical environment. The former
constitutes a consequent progression of micro-oriented modeling, whereas the latter builds
on distributed and online simulation approaches.

多智能体系统在建模和模拟中用作隐喻。在建模级别，它支持将所研究的系统视为交互的自主实体的社区。在仿真级别，它有助于将仿真系统设计为与物理环境交互的分布式并发实体。前者构成了面向微观建模的后续发展，而后者则建立在分布式和在线仿真方法之上。

> The agent metaphor has particularly propelled research on human behavior modeling.
Technical questions such as how to facilitate the modeling and simulation of multiple deliberative
agents, have received a lot of attention (see also Part IV). However, often the more
urgent problem is to find the knowledge and data upon which developing and validating
these models can be based. This problem is addressed in the chapter “Challenges of Country
Modeling Databases, Newsfeeds, and Expert Surveys” by Barry G. Silverman, Gnana K.
Bharathy, and G. Jiyun Kim. Three different sources of knowledge are exploited, i.e., web
corpus of empirical materials, specific domain databases, and questionnaires, to construct
realistic profiles for the actors and issues at play in ethno-political conflict regions. Whereas
in these scenarios detailed models of individual actors play a central role, other applications
are content with comparatively coarse behavior models which describe many individuals.
To those belong crowd and traffic simulation.

代理隐喻特别推动了对人类行为建模的研究。诸如如何促进多个审议代理的建模和模拟等技术问题受到了很多关注（另见第四部分）。然而，通常更紧迫的问题是找到开发和验证这些模型所依据的知识和数据。Barry G. Silverman、Gnana K. Bharathy 和 G. Jiyun Kim 在“国家建模数据库、新闻源和专家调查的挑战”一章中讨论了这个问题。利用三种不同的知识来源，即实证材料的网络语料库、特定领域数据库和问卷，为种族政治冲突地区的参与者和问题构建真实的概况。在这些场景中，单个参与者的详细模型起着核心作用，而其他应用程序则满足于描述许多个体的相对粗糙的行为模型。这些属于人群和交通模拟。

> Crowd simulation is concerned with analyzing the behavior of many individuals in too
little space. This behavior is determined by individual and collective behavior patterns, a
mix of competition for shared space, and collaboration due to, not necessarily explicit but
shared, social norms. The purpose of simulation studies ranges from a better understanding
of certain emergent phenomena to the concrete management of crowds in certain settings.
In the later case, we can further distinguish between offline analysis of the effects of different
infrastructures on crowd behavior and online support to handle specific strategies in crises
situations. Whereas traditionally cellular automata have been exploited for crowd simula-
tion, situated agent-based approaches offer new possibilities as they allow one to treat the
environment and the entities that inhabit it as first class citizens as Stefania Bandini, Sara
Manzoni, and Giuseppe Vizzari describe in the chapter “Crowd Behavior Modeling: From
Cellular Automata to Multi-Agent Systems”.

群体模拟关注的是分析在太小的空间内许多个体的行为。这种行为是由个人和集体的行为模式决定的，对共享空间的竞争，以及由于不一定是明确但共享的社会规范而产生的协作。模拟研究的目的范围从更好地了解某些新兴现象到在某些环境中具体管理人群。在后一种情况下，我们可以进一步区分不同基础设施对人群行为影响的离线分析和在线支持，以在危机情况下处理特定策略。传统上，元胞自动机被用于群体模拟，而基于智能体的定位方法提供了新的可能性，因为它们允许人们将环境和居住在其中的实体视为一等公民，正如 Stefania Bandini、Sara Manzoni 和 Giuseppe Vizzari 在“群体行为建模：从元胞自动机到多智能体系统”一章中所描述的那样。

> Vehicular traffic is another classical example of a multi-agent system: Autonomous agents
(i.e., the drivers) operate in a shared environment which is given by the road infrastructure.
Typically, agent-based models are built on a microscopic modeling approach describing the
motion of each individual vehicle. Scientists described the physical propagation of traffic
flows by means of dynamic models already in the 1950s. Since then the microscopic approach
has grown gradually in popularity because of higher computational power. This development
has been accelerated in the last decade by agent oriented modeling and simulation. In the
chapter “Agents for Traffic Simulation” Arne Kesting, Martin Treiber and Dirk Helbing
provide an overview of the state-of-the-art in traffic modeling and simulation. Detailed
driver models and the implications for an effective and efficient simulation of these micro
models are presented. Entirely new simulation approaches are required when it comes to
using vehicle to vehicle communication and predicting traffic based on incomplete knowledge
quasi online in vehicles.

车辆交通是多智能体系统的另一个典型示例：自主智能体（即驾驶员）在道路基础设施提供的共享环境中运行。通常，基于代理的模型建立在描述每辆车运动的微观建模方法之上。科学家们在 1950 年代就通过动态模型描述了交通流的物理传播。从那时起，由于更高的计算能力，微观方法逐渐受到欢迎。在过去十年中，面向智能体的建模和仿真加速了这一发展。在“交通模拟代理”一章中，Arne Kesting、Martin Treiber 和 Dirk Helbing 概述了交通建模和模拟的最新技术。介绍了详细的驾驶员模型以及对这些微模型进行有效和高效仿真的影响。当涉及到使用车对车通信和基于车辆准在线不完整知识预测交通时，需要全新的仿真方法。

> Symbiotic simulation is one particular form of online simulation, which stresses the joint
benefit of a close interaction between simulation and physical environment for both. This
benefit is due to the data that allow a simulation to adapt itself to more precisely predict
dynamics, the physical environment in turn will benefit from these more reliable predictions.
As this type of simulation is driven by data, there is also a close relation to dynamic
data driven application systems. In the chapter “An Agent-Based Generic Framework for
Symbiotic Simulation” Heiko Aydt, Stephen John Turner, Wentong Cai, and Malcolm Yoke
Hean Low present a range of symbiotic simulation approaches. At the core of designing these
different systems we find the agent metaphor, as the systems comprise multiple, concurrently
active units, whose composition and interaction is highly adaptive and which are in frequent
interaction with the environment.

共生仿真是在线仿真的一种特殊形式，它强调仿真和物理环境之间密切交互对两者的共同好处。这种好处是由于数据允许模拟自我适应以更精确地预测动力学，物理环境反过来也将从这些更可靠的预测中受益。由于这种类型的模拟是由数据驱动的，因此与动态数据驱动的应用程序系统也存在密切关系。在“基于智能体的共生仿真通用框架”一章中，Heiko Aydt、Stephen John Turner、Wentong Cai 和 Malcolm Yoke Hean Low 介绍了一系列共生仿真方法。在设计这些不同系统的核心，我们发现了代理的隐喻，因为这些系统由多个同时活跃的单元组成，其组成和交互具有高度适应性，并且与环境频繁交互。

> Whereas in the above chapters, modeling and simulation of human behavior is at the core
of interest, the chapter on “Agent-Based Modeling of Stem Cells” by Mark d’Inverno, Paul
Howells, Sara Montagna, and Rob Saunders is dedicated to a new emerging area for model-
ing and simulation methods: Systems Biology. Systems Biology brings together researchers
from diverse areas such as Biology, Medicine, Physics, and Computer Science. Thereby, in-
silico experimentation is aimed at complementing wet-lab experimentation. Whereas con-
tinuous, deterministic macro models still prevail, discrete micro models are gaining ground
as well. In this context also agent-oriented approaches receive increasingly attention, as
they allow interpreting biological systems as a community of interacting entities that can
be individually traced. Particularly, in combination with suitable visualization techniques,
agent-based approaches allow a comprehensive and realistic modeling of biological systems
and can reveal new insights into the behavior of complex cellular systems.

在上述章节中，人类行为的建模和模拟是核心兴趣，而 Mark d'Inverno、Paul Howells、Sara Montagna 和 Rob Saunders 的“基于代理的干细胞建模”一章则专门介绍了建模和模拟方法的新兴领域：系统生物学。系统生物学汇集了来自生物学、医学、物理学和计算机科学等不同领域的研究人员。因此，计算机模拟实验旨在补充湿实验室实验。虽然连续的、确定性的宏观模型仍然占主导地位，但离散的微观模型也正在取得进展。在这种情况下，面向代理的方法也越来越受到关注，因为它们允许将生物系统解释为可以单独追踪的相互作用实体的社区。特别是，结合合适的可视化技术，基于智能体的方法允许对生物系统进行全面而真实的建模，并可以揭示对复杂细胞系统行为的新见解。











 