# Tools

> 14. RoboCup Rescue: Challenges and Lessons Learned
> 15. Agent-Based Simulation Using BDI Programming in Jason
> 16. SeSAm: Visual Programming and Participatory Simulation for Agent-Based Models
> 17. JAMES II - Experiences and Interpretations 

14 RoboCup Rescue：挑战和经验教训

15 在 Jason 中使用 BDI 编程进行基于智能体的仿真

16 SeSAm： 基于智能体的模型的可视化编程和参与式仿真

17 JAMES II - 经验和解释


> Agents are used as a metaphor for describing a system of interest. Software agents are
evaluated in virtual dynamic environments. This can be done by testing in small environments 
via so-called test-beds for agents or by testing in large ones, which implies a modeling
of the environment the software agents shall dwell in. All require simulation systems. Often
these environments are built from scratch. However, the re-use of simulation environments
promises less effort, improved repeatability and comparability of experiments. Not surprisingly, 
quite a few simulation systems for multi-agent systems have been built. However, due
to the diversity of agents and objectives of simulation studies, a widely accepted modeling
and simulation approach has remained elusive. The current landscape of agent modeling
and simulation tools reflects the different needs and background of the systems’ developers
equally.

代理用作描述感兴趣系统的隐喻。软件代理用来评估虚拟动态环境。
这可以通过通过所谓的代理测试台在小型环境中进行测试来完成，也可以通过在大型环境中进行测试来完成，
这意味着对软件代理应居住的环境进行建模。所有这些都需要仿真系统。这些环境通常是从头开始构建的。
但是，重复使用仿真环境有望减少工作量，提高实验的可重复性和可比性。
毫不奇怪，已经构建了相当多的多智能体系统的仿真系统。然而，由于仿真研究的主体和目标的多样性，
被广泛接受的建模和仿真方法仍然难以捉摸。代理建模和仿真工具的当前形势同样反映了系统开发人员的不同需求和背景。

> Concrete test-beds, that provide dynamic, standardized scenarios in which different agent
strategies e.g., of deliberation and commitment, mark the beginning of simulation tools for
multi-agent systems in the 80s. With the RoboCupSoccer in 1997 a problem was found that
allowed to examine a wide range of technologies in robotics and artificial intelligence. To
demonstrate that the strategies and evaluations are also viable in other socially relevant
scenarios (a concern that has accompanied work on test-beds from the very beginning) the
RoboCupRescue project was initiated in 2000. The areas of promoted research in disaster-rescue
 comprise multi-agent teamwork coordination, robotics, information infra-structure,
evaluation benchmarks for rescue strategies and simulator development. Thus, the objective
of simulation research in this project is twofold, i.e. to provide a suitable evaluation platform
for those other areas, and to identify requirements and to develop solutions for simulators
to be applied in rescue settings. Tomoichi Takahashi provides insight into this research with
his chapter “Robocup: Challenges and Lessons Learned”.

混凝土测试台提供动态、标准化的场景，其中不同的代理策略（例如深思熟虑和承诺）标志着 80 年代多代理系统模拟工具的开始。
在 1997 年的 RoboCupSoccer 中，发现了一个问题，可以检查机器人和人工智能领域的广泛技术。
为了证明这些策略和评估在其他与社会相关的场景中也是可行的（从一开始就伴随着测试台工作的问题），
RoboCupRescue 项目于 2000 年启动。促进灾害救援研究的领域包括多智能体团队合作协调、机器人技术、信息基础设施、
救援策略评估基准和模拟器开发。因此，本项目中模拟研究的目标是双重的，即为其他领域提供合适的评估平台，
并确定需求并开发适用于救援环境的模拟器解决方案。Tomoichi Takahashi 在他的章节
“Robocup：挑战和经验教训”中提供了对这项研究的见解。

> The aim to support arbitrary scenarios led to the development of general modeling and
simulation systems for multi-agent systems. Whereas reactive agents can easily be described
in simulation systems that support an object-oriented, modular model design, the effective
and efficient handling of multiple deliberative agents provide some challenges for modeling
and simulation environments. Rafael Bordini and Jomi H¨ubner address those in their chapter
“Agent-Based Simulation Using BDI Programming in Jason” by focusing on the description
of deliberative agents in the agent language AgentSpeak. Thereby, they distinguish between
agents with their declarative representations of mental attitudes and display of rational,
goal-directed behavior and the reactive environment the agents are situated in. The latter
is responsible for advancing the simulation.

支持任意场景的目标导致了多智能体系统的通用建模和仿真系统的开发。
虽然在支持面向对象的模块化模型设计的仿真系统中可以很容易地描述反应代理，
但对多个审议代理的有效处理给建模和仿真环境带来了一些挑战。
Rafael Bordini 和 Jomi H ̈ubner 在他们的章节“在 Jason 中使用 BDI 编程进行基于智能体的仿真”
中通过重点介绍智能体语言 AgentSpeak 中对审议智能体的描述来解决这些问题。
因此，它们区分了具有心理态度的陈述性表示和理性、目标导向行为的展示的代理，
以及代理所处的反应性环境。后者负责推进模拟。

> Developing agent and environmental models requires programming in Jason. In contrast,
other agent-based simulation systems offer easy to use interfaces to facilitate agent-based
simulation for domain experts not familiar with programming - a motivation that also
drove the development of expert systems shells in the 1980s. In the chapter “SeSAm (Shell
for Simulated Multi-Agent Systems): Visual Programming and Participatory Simulation for
Agent-Based Models” Franziska Kl¨ugl describes experiences with this type of simulation tool
and the efforts required toward achieving this goal. In this context, the role of adequate
visual means is examined in several interdisciplinary applications. Whereas many agent
simulation systems focus on the encoding of the agents and its environment only, SeSAm
and its user interface address the entire modeling and simulation life cycle: from model
development, experiment design, to the analysis of simulation results.

开发代理和环境模型需要在 Jason 中编程。相比之下，其他基于智能体的仿真系统提供了易于使用的接口，
为不熟悉编程的领域专家提供了基于智能体的仿真 - 这一动机也推动了 1980 年代专家系统 shell 的开发。
在“SeSAm （Shell for Simulated Multi-Agent Systems）：基于代理的模型的可视化编程和参与式模拟”一章中，
Franziska Kl ̈ugl 描述了使用此类模拟工具的经验以及为实现此目标所需的努力。
在这种情况下，在几个跨学科应用中研究了适当的视觉手段的作用。许多智能体仿真系统只关注智能体及其环境的编码，
而 SeSAm 及其用户界面则解决了整个建模和仿真生命周期的问题：从模型开发、实验设计到仿真结果的分析。

> The entire modeling and simulation life cycle is supported in the tool JAMES II, which
first developed as a tool for multi-agent modeling and simulation turned due to the required
flexibility into a “Java multi-purpose environment for simulation”. To support different mod-
eling formalisms, simulation engines, experimental settings, random number generators etc.
a plug-in architecture has been realized which allows an easy extension and adaptation of
the system to new applications. In contrast to other multi-agent simulation systems, JAMES
II supports the description of agents in modeling formalisms with a clear operational se-
mantics being realized by different sequential and parallel simulation engines. The modeling
formalisms are traditional discrete event modeling formalisms which have been extended
to support dynamic patterns of composition and interaction. In the chapter “JAMES II - 
Experiences and Interpretations” Jan Himmelspach and Mathias R¨ohl give an overview
about the architecture of the system, and exemplarily describe the extension of a modeling
formalism, its use for describing agents, and its simulation in JAMES II.

JAMES II 工具支持整个建模和仿真生命周期，该工具最初是作为多智能体建模和仿真工具开发的，
由于所需的灵活性，该工具转变为“用于仿真的 Java 多用途环境”。为了支持不同的模块化形式、
模拟引擎、实验设置、随机数生成器等，实现了一个插件架构，允许系统轻松扩展和适应新的应用程序。
与其他多智能体仿真系统相比，JAMES II 支持在建模形式中对智能体的描述，并通过不同的顺序和并行仿真引擎实现清晰的操作序列。
建模形式是传统的离散事件建模形式，它已被扩展为支持组合和交互的动态模式。
在“JAMES II - 经验和解释”一章中，Jan Himmelspach 和 Mathias R ̈ohl 概述了系统的架构，
并示例性地描述了建模形式主义的扩展、它用于描述代理的用途以及它在 JAMES II 中的模拟。
