# Background

1. Multi-Agent Systems and Simulation: A Survey from the Agent Community’s Perspective ......  3
> Fabien Michel, Jacques Ferber, and Alexis Drogoul
> Introduction • M&S for MAS: The DAI Case • MAS for M&S: Building Artificial
> Laboratories • Simulating MAS: Basic Principles • The Zeigler’s Framework for
> Modeling and Simulation • Studying MAS Simulations Using the Framework for
> M&S • Conclusion
> 

2. Multi-Agent Systems and Simulation: A Survey from an Application Perspective .......... 53
> Klaus G. Troitzsch
> Simulation in the Sciences of Complex Systems • Predecessors and Alternatives
> • Unfolding, Nesting, Coping with Complexity • Issues for Future Research: The
> Emergence of Communication

3. Simulation Engines for Multi-Agent Systems .................... 77
> Georgios K. Theodoropoulos, Rob Minson, Roland Ewald, and Michael Lees
> 
> Introduction • Multi-Agent System Architectures • Discrete Event Simulation En
> gines for MAS • Parallel Simulation Engines for MAS • Issues for Future Research


 ---

> Simulation studies have accompanied the development of multi-agent systems from the beginning.
> Simulation has been used to understand the interaction among agents and between agents and 
> their dynamic environment. The focus has been on test beds, and the description and 
> integration of agents in dynamic virtual environments. Micro and individual-based simulation 
> approaches also became aware of the new possibilities that the agent metaphor and the 
> corresponding methods offer. The area of social simulation played a key role, being enriched 
> and equally challenged by more detailed models of individuals and contributing itself to a 
> better understanding of the effects of cooperation and coordination strategies in multi-agent 
> environments. During the first decade the focus of research has been on the modeling layer. 
> Only gradually, the need to take a closer look at simulation took hold, e.g., 
> how to ensure efficient and repeatable simulation runs.

仿真研究从一开始就伴随着多智能体系统的开发。仿真已用于了解智能体之间以及智能体与其动态环境之间的交互。
重点一直放在测试台上，以及动态虚拟环境中代理的描述和集成。基于微观和个体的仿真方法也意识到代理隐喻和
相应方法提供的新可能性。社会仿真领域发挥了关键作用，它被更详细的个体模型丰富并同样受到挑战，并有助于
更好地理解多智能体环境中合作和协调策略的效果。在第一个十年中，研究的重点一直放在建模层。只是逐渐地，
需要仔细研究仿真，例如，如何确保高效且可重复的仿真运行。

> The chapter by Fabien Michel, Jacque Ferber, and Alexis Drougol on “Multi-agent systems and simulation: A survey from the agent community’s perspective” gives a historical overview of the methodological developments at the interface between multi-agent systems and simulation from an agent’s perspective. The role of test-beds in understanding and analyzing multi-agent systems in the 1980s, the development of abstract agent models, the role of social simulation in promoting research in multi-agent systems and simulation, and the challenges of describing agents and their interactions shape the first decade of research. With the environment of agents becoming an active player, the questions about timing move into focus and with them traditional problems of simulator design, e.g., how to handle concurrent events. For in-depth analysis simulation questions like validity of models, design and evaluation of (stochastic) simulation experiments need to be answered, but also new one emerge in the context of virtual, augmented environments.

Fabien Michel、Jacque Ferber 和 Alexis Drougol 关于“多智能体系统和仿真：智能体社区视角的调查”一章从智能体的角度对多智能体系统和仿真之间接口的方法论发展进行了历史概述。1980 年代测试台在理解和分析多智能体系统方面的作用、抽象智能体模型的开发、社会仿真在促进多智能体系统和仿真研究方面的作用，以及描述智能体及其交互的挑战，塑造了研究的第一个十年。随着 agent 的环境成为活跃的参与者，有关 timing 的问题成为焦点，随之而来的是仿真器设计的传统问题，例如，如何处理并发事件。为了深入分析仿真问题，如模型的有效性、（随机）仿真实验的设计和评估，需要回答这些问题，但在虚拟、增强环境的背景下也会出现新的问题。

> The significant impact of social science on multi-agents research is reflected in the realm of simulation. In the chapter “Multi-Agent Systems and Simulation: A Survey from an Application Perspective,” Klaus Troitzsch traces the first simple agent-based models back to the 1960s. Particularly, analyzing the micro and macro link of social systems, i.e., the process of human actions being (co-) determined by their social environment and at the same time influencing this social environment, permeates agent-based simulation approaches from the beginning, despite the diversity of approaches which manifests itself in varying level of details, number of agents, interaction patterns (e.g., direct or in-direct via the environment), and simulation approach. The aim of these simulation studies is to support or falsify theories about social systems. However, in doing so, they also reveal mechanisms that help to ensure certain desirable properties in a community of autonomous interacting entities and as such can be exploited for the design of software agent communities as proposed by the “socionics” initiative.

社会科学对多智能体研究的重大影响反映在仿真领域。在“多智能体系统和仿真：从应用角度进行调查”一章中，Klaus Troitzsch 将第一个基于智能体的简单模型追溯到 1960 年代。特别是，分析社会系统的微观和宏观联系，即人类行为由其社会环境（共同）决定并同时影响该社会环境的过程，从一开始就渗透到基于代理的仿真方法中，尽管方法的多样性表现为不同的细节级别、代理数量、交互模式（例如， 直接或间接通过环境）和仿真方法。这些仿真研究的目的是支持或证伪有关社会系统的理论。然而，在此过程中，它们也揭示了有助于确保自主交互实体社区中某些理想属性的机制，因此可以被用于“仿生学”倡议提出的软件代理社区的设计。

> A long neglected area of research has been the question of how to execute multi-agent models in an efficient and correct manner. This question is addressed in the chapter by Georgios Theodoropolous, Rob Minson, Roland Ewald, and Michael Lees on “Simulation Engines for Multi-Agent Systems”. Often agent implementations were translated into discrete stepwise “simulation” with no explicit notion of simulation time. However, the need to associate arbitrary time with the behavior of agents and synchronize the behavior of agents with the dynamics of the environment led to discrete event simulation approaches. As the simulation of multiple heavy weight agents require significant computation effort, sequential discrete event simulators are complemented by parallel discrete ones and help an efficient simulation of multi-agent systems. Interestingly, in the opposite direction we find the agent approach exploited to support the distributed simulation of latency simulation systems. Simulation systems are interpreted as agents and the problem of interoperability and synchronization of these simulation systems is translated into terms of communication and coordination.

一个长期被忽视的研究领域是如何以高效和正确的方式执行多智能体模型的问题。Georgios Theodoropolous、Rob Minson、Roland Ewald 和 Michael Lees 在“多智能体系统的仿真引擎”一章中讨论了这个问题。通常，代理实现被转换为离散的逐步 “仿真” ，没有明确的仿真时间概念。然而，需要将任意时间与智能体的行为相关联，并将智能体的行为与环境动态同步，这导致了离散事件仿真方法的出现。由于多个重量级代理的仿真需要大量的计算工作，因此顺序离散事件仿真器由并行离散仿真器补充，有助于高效仿真多智能体系统。有趣的是，在相反的方向上，我们发现 agent 方法被用来支持延迟仿真系统的分布式仿真。仿真系统被解释为代理，这些仿真系统的互操作性和同步问题被转化为通信和协调的术语。

