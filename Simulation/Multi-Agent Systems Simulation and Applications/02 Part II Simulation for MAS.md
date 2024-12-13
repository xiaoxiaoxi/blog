# Simulation for MAS

> - 4 Polyagents: Simulation for Supporting Agents’ Decision Making
> - 5 Combining Simulation and Formal Tools for Developing Self-Organizing MAS
> - 6 On the Role of Software Architecture for Simulating Multi-Agent Systems
> - 7 Replicator Dynamics in Discrete and Continuous Strategy Spaces
> - 8 Stigmergic Cues and Their Uses in Coordination: An Evolutionary Approach

- 4 Polyagents：支持代理决策的仿真 
- 5 结合仿真和形式化工具开发自组织 MAS
- 6 关于软件架构在仿真多智能体系统中的作用
- 7 离散和连续策略空间中的复制器动力学
- 8 激励暗示及其在协调中的应用：一种进化方法

> A typical characteristic of MAS is an inherent distribution of resources. Agents have
only partial access to the environment. System-wide properties result from the local actions
of the agents and their interactions. Because of the distributed nature of MAS, testing
by simulation becomes imperative in the software development process of MAS. Software
agents can also use agent-based simulation to guide their decisions. This way, agents run a
model of the world to see what might happen under various decision alternatives and make
the decision that leads to the most desirable outcome. This part presents five chapters that
show different uses of simulation for MAS.

MAS 的一个典型特征是固有的资源分布。代理只能访问环境的部分权限。系统范围的属性是由代理程序的本地操作及其交互产生的。
由于 MAS 的分布式特性，在 MAS 的软件开发过程中，通过仿真进行测试变得势在必行。软件代理还可以使用基于代理的仿真来指导他们的决策。
通过这种方式，代理运行一个世界模型，看看在各种决策选择下会发生什么，并做出导致最理想结果的决策。
本部分将介绍五章，介绍仿真在 MAS 中的不同用途。

> In “Polyagents: Simulation for Supporting Agents’ Decision Making”, Parunak and
Brueckner, introduce a construct for multi-agent modeling that encapsulates a technique
of simulation-based decision-making. A polyagent represents an entity in the domain. The
polyagent generates a stream of transient ghosts to explore various issues of interest to the
entity. These ghosts can be applied to explore alternative futures, evaluate plan structures,
compare the usefulness of alternative options, etc. Each ghost explores a possible trajectory
for the entity, which then chooses its behavior based on the experiences of its ghosts.

在“Polyagents： Simulation for Supporting Agents' Decisionmaking”中，Parunak 和 Brueckner 介绍了一种多智能体建模结构，该结构封装了一种基于仿真的决策技术。polyagent 表示域中的实体。polyagent 会生成一个瞬态重影流，以探索实体感兴趣的各种问题。这些幽灵可用于探索替代未来、评估计划结构、比较替代选项的有用性等。每个 ghost 都会探索实体的可能轨迹，然后实体会根据其 ghost 的经历来选择其行为。

> In “Combining Simulation and Formal Tools for the Development of Self-Organizing
Multi-Agent Systems”, Luca Gardelli, Mirko Viroli, and Andrea Omicini present a systematic 
use of simulation and formal tools in the early design phase of the development of
self-organizing systems. The authors propose an iterative process consisting of modeling,
simulation, verification, and tuning. Due to the state explosion problem inherent to model
checking, the approach is currently limited to verifying only small instances of systems.
However, the authors show that use of model checking techniques is very useful in the first
iterations on small instances of the problem.

在“结合仿真和形式化工具开发自组织多智能体系统”中，
Luca Gardelli、Mirko Viroli 和 Andrea Omicini 介绍了在自组织系统开发的早期设计阶段系统地使用仿真和形式化工具。
作者提出了一个由建模、仿真、验证和调整组成的迭代过程。由于模型检查固有的状态爆炸问题，
该方法目前仅限于验证系统的小型实例。然而，作者表明，在问题的小型实例的第一次迭代中，使用模型检查技术非常有用。

> Common knowledge in simulation platforms is typically reified in reusable code, libraries,
and software frameworks. In “On the Role of Software Architecture for Simulating Multi-
Agent Systems”, Alexander Helleboogh, Tom Holvoet, and Danny Weyns put forward software
architecture in addition to such code libraries and software frameworks. Software
architecture captures the essence of a simulation platform in an artifact that amplifies reuse
beyond traditional code libraries and software frameworks. It supports consolidating and
sharing expertise in the domain of multi-agent simulation in a form that has proven its
value for software development.

仿真平台中的常识通常具体化为可重用的代码、库和软件框架。
在“论软件架构在仿真多代理系统中的作用”中，Alexander Helleboogh、Tom Holvoet 和 Danny Weyns 
提出了除了此类代码库和软件框架之外的软件架构。软件架构在工件中捕获了仿真平台的精髓，
从而超越了传统代码库和软件框架的重用。它支持以已证明其软件开发价值的形式整合和共享多智能体仿真领域的专业知识。

> In “Replicator Dynamics in Discrete and Continuous Strategy Spaces”, Karl Tuyls and
Ronald Westra study multi-agent evolutionary dynamics from a game theoretic perspective.
The authors simulate and analyze the properties and asymptotic behavior of multi-agent
games with discrete and continuous strategy spaces. To this end they use existing models
of the replicator dynamics and introduce a new replicator dynamics model for continuous
strategy spaces. Experiments show that the new model outperforms existing models in a
simple game.

在“离散和连续策略空间中的复制器动力学”中，Karl Tuyls 和 Ronald Westra 从博弈论的角度研究了多代理进化动力学。
作者仿真并分析了具有离散和连续策略空间的多智能体博弈的属性和渐近行为。
为此，他们使用了现有的复制器动力学模型，并为连续策略空间引入了新的复制器动力学模型。
实验表明，新模型在简单游戏中的性能优于现有模型。

 
> Finally, in “Stigmergic Cues and Their Uses in Coordination: an Evolutionary Approach”,
Luca Tummolini, Marco Mirolli, and Cristiano Castelfranchi, explore the evolution of stig-
mergic behavior adopting a simulative approach. The authors simulate a population of
artificial agents living in a virtual environment containing safe and poisonous fruits. The
behavior of the agents is governed by artificial neural networks whose free parameters (i.e.
the weights of the networks’ connections) are encoded in the genome of the agents and
evolve through a genetic algorithm. By making the transition from a MAS in which agents
individually look for resources to one in which each agent indirectly coordinates with what
the other agents do (stigmergic self-adjustment) and, finally, to a situation in which each
agent sends a message about what kind of resources are available (stigmergic communica-
tion), the simulations offer a precise analysis of the difference between traces that are signs
with a behavioral content and traces that are signals with a behavioral message.

最后，在“激励暗示及其在协调中的用途：一种进化方法”中，Luca Tummolini、Marco Mirolli 和 
Cristiano Castelfranchi 探讨了采用仿真方法的耻辱行为的演变。
作者仿真了生活在包含安全和有毒水果的虚拟环境中的人工代理群体。
代理的行为由人工神经网络控制，其自由参数（即网络连接的权重）编码在代理的基因组中，并通过遗传算法进化。
通过从智能体单独寻找资源的 MAS 过渡到每个智能体间接与其他智能体所做的事情协调（耻辱性自我调整），
最后，过渡到每个智能体发送关于可用资源类型的信息（耻辱性通信）的情况，
仿真提供了对具有行为内容的标志的痕迹和作为信号的痕迹之间的差异的精确分析带有行为信息。


