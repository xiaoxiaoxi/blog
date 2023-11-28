# 基于智能体的建模和仿真教程 Tutorial on agent-based modeling and simulation

> <b> CM Macal and MJ North</b>

> Center for Complex Adaptive Agent Systems Simulation, Decision & Information Sciences Division, Argonne National Laboratory, Argonne, Il, USA; and Computation Institute, The University of Chicago, Chicago, Il, USA
 
 美国伊利诺伊州阿贡市阿贡国家实验室决策与信息科学部复杂自适应智能体系统仿真中心;和芝加哥大学计算研究所，美国伊利诺伊州芝加哥

> Agent-based modeling and simulation (ABMS) is a relatively new approach to modeling systems composed of autonomous, interacting agents. Agent-based modeling is a way to model the dynamics of complex systems and complex adaptive systems. Such systems often self-organize themselves and create emergent order. Agent-based models also include models of behaviour (human or otherwise) and are used to observe the collective effects of agent behaviours and interactions. The development of agent modeling tools, the availability of micro-data, and advances in computation have made possible a growing number of agent-based applications across a variety of domains and disciplines. This article provides a brief introduction to ABMS, illustrates the main concepts and foundations, discusses some recent applications across a variety of disciplines, and identifies methods and toolkits for developing agent models.

基于智能体的建模和仿真 （ABMS） 是一种相对较新的方法，用于对由自主交互智能体组成的系统进行建模。基于智能体的建模是一种对复杂系统和复杂自适应系统的动力学进行建模的方法。这样的系统经常自我组织并创造紧急秩序。基于智能体的模型还包括行为模型（人类或其他），用于观察智能体行为和互动的集体效应。智能体建模工具的发展、微数据的可用性以及计算的进步使越来越多的基于智能体的应用成为可能，这些应用跨越了各种领域和学科。本文简要介绍了 ABMS，说明了主要概念和基础，讨论了跨各种学科的一些最新应用，并确定了开发代理模型的方法和工具包。

## 1. Introduction 

> Agent-based modeling and simulation (ABMS) is a relatively new approach to modeling complex systems composed of interacting, autonomous ‘agents’. Agents have behaviours, often described by simple rules, and interactions with other agents, which in turn influence their behaviours. By modeling agents individually, the full effects of the diversity that exists among agents in their attributes and behaviours can be observed as it gives rise to the behaviour of the system as a whole. By modeling systems from the ‘ground up’—agent-by-agent and interaction-by-interaction—self-organization can often be observed in such models. Patterns, structures, and behaviours emerge that were not explicitly programmed into the models, but arise through the agent interactions. The emphasis on modeling the heterogeneity of agents across a population and the emergence of self-organization are two of the distinguishing features of agent-based simulation as compared to other simulation techniques such as discrete-event simulation and system dynamics. Agent-based modeling offers a way to model social systems that are composed of agents who interact with and influence each other, learn from their experiences, and adapt their behaviours so they are better suited to their environment.

基于智能体的建模和仿真 （ABMS） 是一种相对较新的方法，用于对由交互式自主“智能体”组成的复杂系统进行建模。智能体的行为通常由简单的规则描述，以及与其他智能体的互动，这反过来又会影响他们的行为。通过单独对智能体进行建模，可以观察到智能体之间在属性和行为中存在的多样性的全部影响，因为它导致了整个系统的行为。通过从头开始对系统进行建模——逐个代理和逐个交互——通常可以在此类模型中观察到自组织。模式、结构和行为的出现没有明确地编程到模型中，而是通过智能体交互产生的。与其他模拟技术（如离散事件模拟和系统动力学）相比，强调对群体中智能体的异质性进行建模和自组织的出现是基于智能体的模拟的两个显着特征。基于智能体的建模提供了一种对社会系统进行建模的方法，这些社会系统由智能体组成，这些智能体相互影响和影响，从他们的经验中学习，并调整他们的行为，使他们更好地适应他们的环境。

> Applications of agent-based modeling span a broad range of areas and disciplines. Applications range from modeling agent behaviour in the stock market (Arthur et al, 1997) and supply chains (Macal, 2004a) to predicting the spread of epidemics (Bagni et al, 2002) and the threat of bio-warfare (Carley et al, 2006), from modeling the adaptive immune system (Folcik et al, 2007) to understanding consumer purchasing behaviour (North et al, 2009), from understanding the fall of ancient civilizations (Kohler et al, 2005) to modeling the engagement of forces on the battlefield (Moffat et al, 2006) or at sea (Hill et al, 2006), and many others. Some of these applications are small but elegant models, which include only the essential details of a system, and are aimed at developing insights into a social process or behaviour. Other agent-based models are large scale in nature, in which a system is modeled in great detail, meaning detailed data are used, the models have been validated, and the results are intended to inform policies and decision making. These applications have been made possible by advances in the development of specialized agent-based modeling software, new approaches to agent-based model development, the availability of data at increasing levels of granularity, and advancements in computer performance.

基于智能体的建模的应用涵盖了广泛的领域和学科。应用范围从模拟股票市场（Arthur et al， 1997）和供应链（Macal， 2004a）中的代理行为，到预测流行病的传播（Bagni et al， 2002）和生物战的威胁（Carley et al， 2006），从模拟适应性免疫系统（Folcik et al， 2007）到了解消费者的购买行为（North et al， 2009），从了解古代文明的衰落（Kohler et al， 2005）到模拟战场上的部队交战（Moffat et al， 2006）或海上（Hill et al， 2006）等等。其中一些应用程序是小而优雅的模型，仅包含系统的基本细节，旨在开发对社会过程或行为的见解。其他基于智能体的模型本质上是大规模的，其中系统被非常详细地建模，这意味着使用详细的数据，模型已经过验证，结果旨在为政策和决策提供信息。这些应用之所以成为可能，是因为基于智能体的专用建模软件的开发、基于智能体的模型开发的新方法、粒度不断提高的数据可用性以及计算机性能的进步。

> Several indicators of the growing interest in agent-based modeling include the number of conferences and workshops devoted entirely to or having tracks on agent-based modeling, the growing number of peer-reviewed publications in discipline-specific academic journals across a wide range of application areas as well as in modeling and simulation journals, the growing number of openings for people specializing in agent-based modeling, and interest on the part of funding agencies in supporting programmes that require agent-based models. For example, a perusal of the programme for a recent Winter Simulation Conference revealed that 27 papers had the word ‘agent’ in the title or abstract (see http://www.wintersim.org/pastprog.htm).

对基于智能体的建模日益增长的兴趣的几个指标包括完全致力于或跟踪基于智能体的建模的会议和研讨会的数量，在广泛的应用领域以及建模和仿真期刊的特定学科学术期刊上发表的同行评审出版物数量不断增加，越来越多的基于智能体建模的专门人员的职位空缺， 以及供资机构对支持需要基于代理的模式的计划的兴趣。例如，仔细阅读最近一次冬季模拟会议的议程发现，有27篇论文的标题或摘要中有“代理人”一词（见 http://www.wintersim.org/pastprog.htm）。

## Agent-based modeling

### 2.1 Agent-based modeling and complexity 

> ABMS can be traced to investigations into complex systems (Weisbuch, 1991), complex adaptive systems (Kauffman, 1993; Holland, 1995), and artificial life (Langton, 1989), known as ALife (see Macal (2009) for a review of the influences of investigations into artificial life on the development of agent-based modeling and the article by Heath and Hill in this issue for a review of other early influences). Complex systems consist of interacting, autonomous components; complex adaptive systems have the additional capability for agents to adapt at the individual or population levels. These collective investigations into complex systems sought to identify universal principles of such systems, such as the basis for self-organization, emergent phenomenon, and the origins of adaptation in nature. ABMS began largely as the set of ideas, techniques, and tools for implementing computational models of complex adaptive systems. Many of the early agent-based models were developed using the Swarm modeling software designed by Langton and others to model ALife (Minar et al, 1996). Initially, agent behaviours were modeled using exceedingly simple rules that still led to exceedingly complex emergent behaviours. In the past 10 years or so, available agent-based modeling software tools and development environments have expanded considerably in both numbers and capabilities.

ABMS可以追溯到对复杂系统（Weisbuch，1991），复杂自适应系统（Kauffman，1993;Holland， 1995）和人工生命（Langton， 1989），称为ALife（参见Macal （2009）对人工生命研究对基于智能体的建模发展的影响的回顾，以及Heath和Hill在本期中的文章对其他早期影响的回顾）。复杂系统由相互作用的自主组件组成;复杂的适应性系统具有代理在个体或群体水平上适应的额外能力。这些对复杂系统的集体调查试图确定这些系统的普遍原则，例如自组织的基础、涌现现象和自然界适应的起源。ABMS最初是一套用于实现复杂自适应系统计算模型的想法、技术和工具。许多早期基于智能体的模型是使用 Langton 等人设计的 Swarm 建模软件开发的，用于对 ALife 进行建模（Minar 等人，1996 年）。最初，智能体行为是使用极其简单的规则建模的，这些规则仍然导致极其复杂的紧急行为。在过去 10 年左右的时间里，可用的基于智能体的建模软件工具和开发环境在数量和功能上都得到了极大的扩展。

> Following the conventional definition of simulation, we use the term ABMS in this article to refer to both agent-based simulation, in which a dynamic and time-dependent process is modeled, and more general kinds of agent-based modeling that includes models designed to do optimization (see, eg, Olariu and Zomaya, 2006) or search (see, eg, Hill et al, 2006). For example, particle swarm optimization and ant optimization algorithms are both inspired by agent-based modeling approaches and are used to achieve an end (optimal) state rather than to investigate a dynamic process, as in a simulation.

遵循模拟的传统定义，我们在本文中使用术语ABMS来指代基于智能体的模拟，其中对动态和时间依赖的过程进行建模，以及更通用的基于智能体的建模，包括旨在进行优化的模型（参见，例如，Olariu和Zomaya，2006）或搜索（参见，例如，Hill等人， 例如，粒子群优化和蚂蚁优化算法都受到基于智能体的建模方法的启发，用于实现最终（最佳）状态，而不是像模拟那样研究动态过程。

### 2.2 Structure of an agent-based model 基于智能体模型的结构

> A typical agent-based model has three elements:
> 1. A set of agents, their attributes and behaviours.
> 2. A set of agent relationships and methods of interaction: An underlying topology of connectedness defines how and with whom agents interact.
> 3. The agents’ environment: Agents interact with their environment in addition to other agents.

典型的基于智能体的模型有三个元素：
1. 一组代理，它们的属性和行为。
2. 一组代理关系和交互方法：连接性的基础拓扑定义了代理交互的方式和对象。
3. 代理的环境：除了其他代理之外，代理还与其环境交互。

> A model developer must identify, model, and program these elements to create an agent-based model. The structure of a typical agent-based model is shown in Figure 2.1. Each of the components in Figure 2.1 is discussed in this section. A computational engine for simulating agent behaviours and agent interactions is then needed to make the model run. An agent-based modeling toolkit, programming language or other implementation provides this capability. To run an agent-based model is to have agents repeatedly execute their behaviours and interactions. This process often does, but is not necessarily modeled to, operate over a timeline, as in time-stepped, activity-based, or discrete-event simulation structures.

模型开发人员必须对这些元素进行识别、建模和编程，以创建基于代理的模型。典型的基于智能体的模型的结构如图 2.1 所示。本节将讨论图 2.1 中的每个组件。然后需要一个用于模拟智能体行为和智能体交互的计算引擎来使模型运行。基于代理的建模工具包、编程语言或其他实现提供了此功能。运行基于智能体的模型就是让智能体重复执行其行为和交互。此过程通常（但不一定建模为）在时间轴上运行，例如在时间步长、基于活动或离散事件的模拟结构中。

> Figure 2.1 The structure of a typical agent-based model, as in Sugarscape (Epstein and Axtell, 1996)
> 
> ![tutorial_ABMS_figure_2_1.png](tutorial_ABMS_figure_2_1.png)

### 2.3 Autonomous agents / 自主代理

> The single most important defining characteristic of an agent is its capability to act autonomously, that is, to act on its own without external direction in response to situations it encounters. Agents are endowed with behaviours that allow them to make independent decisions. Typically, agents are active, initiating their actions to achieve their internal goals, rather than merely passive, reactively responding to other agents and the environment.

智能体最重要的一个定义特征是它能够自主行动，也就是说，在没有外部指导的情况下自行行动以应对它遇到的情况。代理人被赋予了能够做出独立决定的行为。通常，智能体是主动的，发起他们的行动以实现其内部目标，而不仅仅是被动的，被动地响应其他智能体和环境。

> There is no universal agreement in the literature on the precise definition of an agent beyond the essential property of autonomy. Jennings (2000) provides a computer science definition of agent that emphasizes the essential characteristic of autonomous behaviour. Some authors consider any type of independent component (software, model, individual, etc) to be an agent (Bonabeau, 2001). In this view, a component’s behaviour can range from simplistic and reactive ‘if-then’ rules to complex behaviours modeled by adaptive artificial intelligence techniques. Other authors insist that a component’s behaviour must be adaptive, able to learn and change its behaviours in response to its experiences, to be called an agent. Casti (1997) argues that agents should contain both base-level rules for behaviour and higher-level rules that are in effect ‘rules to change the rules’. The base-level rules provide more passive responses to the environment, whereas the ‘rules to change the rules’ provide more active, adaptive capabilities.

在文献中，除了自治的基本属性之外，关于代理人的精确定义没有普遍的共识。Jennings（2000）提供了智能体的计算机科学定义，强调了自主行为的基本特征。一些作者认为任何类型的独立组件（软件、模型、个人等）都是代理（Bonabeau，2001）。在这种观点中，组件的行为范围可以从简单和反应性的“如果-那么”规则到由自适应人工智能技术建模的复杂行为。其他作者坚持认为，组件的行为必须是适应性的，能够学习和改变其行为以响应其经验，才能被称为代理。Casti（1997）认为，智能体应该包含行为的基本规则和更高层次的规则，这些规则实际上是“改变规则的规则”。基本规则提供对环境的更被动响应，而“更改规则的规则”则提供更主动的自适应功能。

> From a practical modeling standpoint, based on how and why agent-models are actually built and described in applications, we consider agents to have certain essential characteristics:

从实际建模的角度来看，基于在应用程序中实际构建和描述智能体模型的方式和原因，我们认为智能体具有某些基本特征：

> - An agent is a `self-contained`, modular, and uniquely identifiable individual. The modularity requirement implies that an agent has a boundary. One can easily determine whether something is part of an agent, is not part of an agent, or is a shared attribute. Agents have attributes that allow the agents to be distinguished from and recognized by other agents.

- 代理是一个`独立的`、模块化的、唯一可识别的个体。模块化要求意味着代理具有边界。人们可以很容易地确定某物是代理的一部分，还是不是代理的一部分，或者是共享属性。代理具有允许代理与其他代理区分开来并被其他代理识别的属性。

> - An agent is `autonomous` and self-directed. An agent can function independently in its environment and in its interactions with other agents, at least over a limited range of situations that are of interest in the model. An agent has behaviours that relate information sensed by the agent to its decisions and actions. An agent’s information comes through interactions with other agents and with the environment. An agent’s behaviour can be specified by anything from simple rules to abstract models, such as neural networks or genetic programs that relate agent inputs to outputs through adaptive mechanisms.

- 代理是`自主`的和自我导向的。智能体可以在其环境中以及与其他智能体的交互中独立运行，至少在模型中感兴趣的有限范围内是这样。智能体的行为将智能体感知到的信息与其决策和行动相关联。代理的信息来自与其他代理和环境的交互。智能体的行为可以由任何内容来指定，从简单的规则到抽象的模型，例如通过自适应机制将智能体输入与输出相关联的神经网络或遗传程序。

> - An agent has a `state` that varies over time. Just as a system has a state consisting of the collection of its state variables, an agent also has a state that represents the essential variables associated with its current situation. An agent’s state consists of a set or subset of its attributes. The state of an agent-based model is the collective states of all the agents along with the state of the environment. An agent’s behaviours are conditioned on its state. As such, the richer the set of an agent’s possible states, the richer the set of behaviours that an agent can have. In an agent-based simulation, the state at any time is all the information needed to move the system from that point forward.

- 代理的 `状态` 随时间而变化。正如系统具有由其状态变量集合组成的状态一样，代理也具有表示与其当前情况相关的基本变量的状态。代理的状态由其属性的集合或子集组成。基于智能体的模型的状态是所有智能体的集合状态以及环境的状态。智能体的行为取决于其状态。因此，智能体的可能状态集越丰富，智能体可以拥有的行为集就越丰富。在基于智能体的模拟中，任何时候的状态都是将系统从该点向前移动所需的所有信息。

> - An agent is `social` having dynamic interactions with other agents that influence its behaviour. Agents have protocols for interaction with other agents, such as for communication, movement and contention for space, the capability to respond to the environment, and others. Agents have the ability to recognize and distinguish the traits of other agents.

- 智能体是具有`社交`性的，与其他智能体进行动态交互，从而影响其行为。智能体具有与其他智能体交互的协议，例如通信、移动和空间争用、对环境的响应能力等。智能体具有识别和区分其他智能体特征的能力。

> Agents may also have other useful characteristics:

代理还可能具有(一些)其他有用的特征：

> - An agent may be `adaptive`, for example, by having rules or more abstract mechanisms that modify its behaviours. An agent may have the ability to learn and adapt its behaviours based on its accumulated experiences. Learning requires some form of memory. In addition to adaptation at the individual level, populations of agents may be adaptive through the process of selection, as individuals better suited to the environment proportionately increase in numbers.

- 智能体可能具有`自适应性`，例如，通过具有规则或更抽象的机制来修改其行为。智能体可能有能力根据其积累的经验学习和调整其行为。学习需要某种形式的记忆。除了个体层面的适应外，主体种群还可以通过选择过程进行适应，因为更适合环境的个体数量成比例地增加。

> - An agent may be `goal-directed`, having goals to achieve (not necessarily objectives to maximize) with respect to its behaviours. This allows an agent to compare the outcome of its behaviours relative to its goals and adjust its responses and behaviours in future interactions.

- 智能体可能是以`目标为导向`的，在其行为方面有要实现的目标（不一定是最大化的目标）。这允许智能体将其行为的结果与其目标进行比较，并在未来的交互中调整其反应和行为。

> Agents may be `heterogeneous`. Unlike particle simulation that considers relatively homogeneous particles, such as idealized gas particles, or molecular dynamics simulations that model individual molecules and their interactions, agent simulations often consider the full range of agent diversity across a population. Agent characteristics and behaviours may vary in their extent and sophistication, how much information is considered in the agent’s decisions, the agent’s internal models of the external world, the agent’s view of the possible reactions of other agents in response to its actions, and the extent of memory of past events the agent retains and uses in making its decisions. Agents may also be endowed with different amounts of resources or accumulate different levels of resources as a result of agent interactions, further differentiating agents.

- 代理可能是`异质的`。与考虑相对均匀粒子（如理想化气体粒子）的粒子模拟或模拟单个分子及其相互作用的分子动力学模拟不同，智能体模拟通常考虑整个群体中所有智能体多样性。智能体的特征和行为可能在其程度和复杂程度、智能体的决策中考虑了多少信息、智能体对外部世界的内部模型、智能体对其他智能体对其行为的反应的可能反应的看法，以及智能体在做出决策时保留和使用的对过去事件的记忆程度。由于智能体的相互作用，智能体还可以被赋予不同数量的资源或积累不同水平的资源，从而进一步区分智能体。

> A typical agent structure is illustrated in Figure 2.2. In an agent-based model, everything associated with an agent is either an agent attribute or an agent method that operates on the agent. Agent attributes can be static, not changeable during the simulation, or dynamic, changeable as the simulation progresses. For example, a static attribute is an agent’s name; a dynamic attribute is an agent’s memory of past interactions. Agent methods include behaviours, such as rules or more abstract representations such as neural networks, which link the agent’s situation with its action or set of potential actions. An example is the method that an agent uses to identify its neighbours.

典型的智能体结构如图 2.2 所示。在基于代理的模型中，与代理关联的所有内容要么是代理属性，要么是对代理进行操作的代理方法。智能体属性可以是静态的，在模拟过程中不可更改，也可以是动态的，随着模拟的进行而改变。例如，静态属性是代理的名称;动态属性是智能体对过去交互的记忆。代理方法包括行为（如规则）或更抽象的表示（如神经网络），它们将代理的情况与其动作或一组潜在动作联系起来。例如，代理用于标识其邻居的方法。

> A theory of agent behaviour for the situations or contexts the agent encounters in the model is needed to model agent behaviour. One may begin with a normative model in which agents attempt to optimize profits, utility, etc, as a starting point for developing a simpler, more descriptive, but realistic, heuristic model of behaviour. One may also begin with a behavioural model if there is available behavioural theory and empirical data to support the application. For example, numerous theories and empirically based heuristics exist for modeling consumer shopping behaviour. These could be implemented and compared in an agent-based model. Cognitive science and related disciplines focus on agents and their social behaviours (Sun, 2006). Behavioural modeling frameworks such as BDI (Belief-Desire-Intent) combine modal and temporal logics as the basis for reactive planning and agent action selection (Wooldridge, 2000). In agent-based modeling applications in which learning is important, theories of learning by individual agents or collectives of agents become important. The field of machine learning is another source of learning algorithms for recognizing patterns in data (such as data mining) through techniques such as supervised learning, unsupervised learning, and reinforcement learning (Alpayd yn, 2004; Bishop, 2007). Genetic algorithms (Goldberg, 1989) and related techniques such as learning classifier systems (Holland et al, 2000) are also commonly used in agent-based models.

需要针对代理在模型中遇到的情境或上下文的代理行为理论来模拟代理行为。人们可以从一个规范模型开始，在这个模型中，代理人试图优化利润、效用等，作为开发一个更简单、更具描述性但现实的启发式行为模型的起点。如果有可用的行为理论和经验数据来支持该应用，也可以从行为模型开始。例如，有许多理论和基于经验的启发式方法可用于对消费者购物行为进行建模。这些可以在基于智能体的模型中实现和比较。认知科学和相关学科专注于智能体及其社会行为（Sun，2006）。行为建模框架，如BDI（信念-欲望-意图）将模态和时间逻辑结合起来，作为反应性计划和代理行动选择的基础（Wooldridge，2000）。在基于智能体的建模应用中，学习很重要，单个智能体或智能体集体的学习理论变得很重要。机器学习领域是学习算法的另一个来源，用于通过监督学习、无监督学习和强化学习等技术识别数据模式（例如数据挖掘）（Alpayd yn，2004;Bishop，2007 年）。遗传算法（Goldberg，1989）和相关技术，如学习分类器系统（Holland等人，2000）也常用于基于智能体的模型。

> Figure 2.2 A typical agent
> 
> ![tutorial_ABMS_figure_2_2.png](tutorial_ABMS_figure_2_2.png)
 
### 2.4 Interacting agents

> Agent-based modeling concerns itself with modeling agent relationships and interactions as much as it does modeling agent behaviours. The two primary issues of modeling agent interactions are specifying who is, or could be, connected to who, and the mechanisms of the dynamics of the interactions. Both aspects must be addressed in developing agent-based models.

基于智能体的建模既关注智能体行为的建模，也关注智能体关系和交互的建模。对智能体交互进行建模的两个主要问题是指定谁与谁有关，或者可能与谁有关，以及交互动态的机制。在开发基于智能体的模型时，必须解决这两个方面。

> One of the tenets of complex systems and agent-based modeling is that only `local information` is available to an agent. Agent-based systems are decentralized systems. There is no central authority that either pushes out globally available information to all agents or controls their behaviour in an effort to optimize system performance. Agents interact with other agents, but not all agents interact directly with all the other agents all the time, just as in real-world systems. Agents typically interact with a subset of other agents, termed the agent’s neighbours. Local information is obtained from interactions with an agent’s neighbours (not any agent or all agents) and from its localized environment (not from any part of the entire environment). Generally, an agent’s set of neighbours changes rapidly as a simulation proceeds and agents move through space.

复杂系统和基于智能体的建模的原则之一是，智能体只能获得`本地信息`。基于代理的系统是去中心化系统。没有一个中央机构可以向所有代理推送全球可用的信息，或者控制他们的行为以优化系统性能。代理与其他代理交互，但并非所有代理都始终直接与所有其他代理交互，就像在现实世界的系统中一样。代理通常与其他代理的子集（称为代理的邻居）进行交互。本地信息是通过与代理的邻居（不是任何代理或所有代理）的交互以及从其本地化环境（而不是从整个环境的任何部分）获取的。通常，随着模拟的进行和智能体在空间中的移动，智能体的邻居集会迅速变化。

> How agents are connected to each other is generally termed an agent-based model’s `topology` or connectedness. Typical topologies include a spatial grid or network of nodes (agents) and links (relationships). A topology describes who transfers information to whom. In some applications, agents interact according to multiple topologies. For example, a recent agent-based pandemic model has agents interacting over a spatial grid to model physical contact as agents go through daily activities and possibly pass on infections. Agents also are members of social networks that model the likelihood of contact with relatives and friends.

代理之间的连接方式通常称为基于代理的模型的`拓扑`或连接性。典型的拓扑包括节点（代理）和链接（关系）的空间网格或网络。拓扑描述谁将信息传输给谁。在某些应用程序中，代理根据多个拓扑进行交互。例如，最近基于智能体的大流行模型让智能体通过空间网格进行交互，以模拟智能体在日常活动和可能传播感染时的身体接触。代理也是社交网络的成员，这些社交网络模拟了与亲戚和朋友联系的可能性。

> An agent’s `neighbourhood` is a general concept applicable to whatever agent spaces are defined in the model. For example, an agent could interact only with its neighbours located close-by in physical (or geographical) space as well as neighbour agents located close-by in its social space as specified by the agent’s social network.

智能体`邻居/相邻`一个通用概念，适用于模型中定义的任何智能体空间。例如，代理只能与位于物理（或地理）空间中的邻居以及位于其社交空间附近的邻居进行交互，这是由代理的社交网络指定的。

> Originally, spatial agent-based models were implemented in the form of cellular automata (CA). Conway’s Game of Life (Gardner, 1970) is a good example. CA represent agent interaction patterns and available local informa- tion by using a grid or lattice environment. The cells immediately surrounding an agent are its neighbourhood. Each cell can be interpreted as an agent that interacts with a fixed set of neighbouring cells. The cell (agent) state is either ‘on’ or ‘off’ at any time. Most early spatial agent-based models had the form of a CA. Epstein and Axtell’s Sugarscape model is an example (Epstein and Axtell, 1996). In Sugarscape, the topology was more complex than in a simple CA. Agents were mobile and able to move from cell to cell. The grid essentially became the agents’ environment. Agents were able to acquire resources from the environment that were distributed spatially across the grid.

最初，基于空间代理的模型是以单元自动机 （CA） 的形式实现的。Conway 的 Game of Life（Gardner，1970）就是一个很好的例子。CA 通过使用网格或格子环境来表示智能体交互模式和可用的本地信息。紧邻病原体的细胞是其邻域。每个细胞都可以解释为与一组固定的相邻细胞相互作用的代理。单元（代理）状态随时为“打开”或“关闭”。Epstein 和 Axtell 的 Sugarscape 模型就是一个例子（Epstein 和 Axtell，1996 年）。在 Sugarscape 中，拓扑结构比简单的 CA 更复杂。 代理是可移动的，能够从一个单元移动到另一个单元。网格基本上成为了智能体的环境。代理能够从环境中获取资源，这些资源在空间上分布在网格中。

> Other agent interaction topologies are now commonly used for modeling agent interactions (Figure 2.3). In the CA model, agents move from cell to cell on a grid and no more than a single agent occupies a cell at one time. The von Neumann ‘5-neighbour’ neighbourhood is shown in Figure 2.3a; the ‘9-neighbour’ Moore neighbourhood is also common. In the Euclidean space model, agents roam in two, three or higher dimensional spaces (Figure 2.3b). Networks allow an agent’s neighbourhood to be defined more generally. For the network topology, networks may be static or dynamic (Figure 2.3c). In static networks, links are pre-specified and do not change. For dynamic networks, links, and possibly nodes, are determined endogenously according to the mechanisms programmed in the model. In the geographic information system (GIS) topology, agents move from patch to patch over a realistic geo-spatial landscape (Figure 2.3d). In the ‘soup’, or aspatial model, agents have no location because it is not important (Figure 2.3e); pairs of agents are randomly selected for interaction and then returned to the soup as candidates for future selection. Many agent-based models include agents interacting in multiple topologies.

其他智能体交互拓扑现在通常用于对智能体交互进行建模（图 2.3）。在 CA 模型中，智能体在网格上从一个单元移动到另一个单元，并且一次不超过一个智能体占用一个单元。冯·诺依曼的“五邻”邻域如图2.3a所示;“9 个邻居”摩尔社区也很常见。在欧几里得空间模型中，智能体在二维、三维或更高维空间中漫游（图2.3b）。网络允许更普遍地定义代理的邻域。对于网络拓扑，网络可以是静态的，也可以是动态的（图 2.3c）。在静态网络中，链接是预先指定的，不会更改。对于动态网络，链路和可能的节点是根据模型中编程的机制内生确定的。在地理信息系统 （GIS） 拓扑中，代理在真实的地理空间景观上从一个 patch 移动到另一个 patch （图 2.3d）。在“soup”或空间模型中，智能体没有位置，因为它不重要（图 2.3e）;随机选择成对的代理进行交互，然后作为未来选择的候选者返回soup中。许多基于代理的模型包括在多个拓扑中交互的代理。

> Figure 2.3 Topologies for agent relationships and social interaction
> 
> ![tutorial_ABMS_figure_2_3.png](tutorial_ABMS_figure_2_3.png)

### 2.5 Agent environment

> Agents interact with their environment and with other agents. The environment may simply be used to provide information on the spatial location of an agent relative to other agents or it may provide a rich set of geographic information, as in a GIS. An agent’s location, included as a dynamic attribute, is sometimes needed to track agents as they move across a landscape, contend for space, acquire resources, and encounter other situations. Complex environ- mental models can be used to model the agents’ environment. For example, hydrology or atmospheric dispersion models can provide point location- specific data on groundwater levels or atmospheric pollutants, respectively, which are accessible by agents. The environment may thus constrain agent actions. For example, the environment in an agent-based transportation model would include the infrastructure and capacities of the nodes and links of the road network. These capacities would create congestion effects (reduced travel speeds) and limit the number of agents moving through the transportation network at any given time.

代理与其环境和其他代理进行交互。环境可以简单地用于提供有关一个智能体相对于其他智能体的空间位置的信息，或者它可以提供一组丰富的地理信息，如在 GIS 中。有时需要智能体的位置作为动态属性包含在内，以跟踪智能体在景观中移动、争夺空间、获取资源以及遇到其他情况。复杂的环境模型可用于对智能体的环境进行建模。例如，水文或大气扩散模型可以分别提供地下水位或大气污染物的点位置特定数据，这些数据可由代理访问。因此，环境可能会限制代理行为。例如，基于智能体的交通模型中的环境将包括道路网络节点和链接的基础设施和容量。这些容量将产生拥堵效应（降低行驶速度），并限制在任何给定时间通过运输网络的代理数量。

## 3 Agent-based modeling applications

### 3.1 The nature of agent-based model applications / 基于智能体的模型应用程序的特性

> Agent-based modeling has been used in an enormous variety of applications spanning the physical, biological, social, and management sciences. Applica- tions range from modeling ancient civilizations that have been gone for hundreds of years to modeling how to design new markets that do not currently exist. Several agent-based modeling applications are summarized in this section, but the list is only a small sampling. Several of the papers covered here make the case that agent-based modeling, versus other modeling techniques is necessary because agent-based models can explicitly model the complexity arising from individual actions and interactions that exist in the real world.

基于智能体的建模已被用于物理、生物、社会和管理科学的各种应用中。应用范围从对已经消失了几百年的古代文明进行建模，到对如何设计目前不存在的新市场进行建模。本节总结了几个基于智能体的建模应用程序，但列表只是一个小样本。这里介绍的几篇论文表明，与其他建模技术相比，基于智能体的建模是必要的，因为基于智能体的模型可以显式地模拟现实世界中存在的单个操作和交互所产生的复杂性。

> Agent-based model structure spans a continuum, from elegant, minimalist academic models to large-scale decision support systems. Minimalist models are based on a set of idealized assumptions, designed to capture only the most salient features of a system. Decision support models tend to serve large-scale applications, are designed to answer real-world policy questions, include real data, and have passed appropriate validation tests to establish credibility.

基于智能体的模型结构跨越了一个连续体，从优雅、极简的学术模型到大规模的决策支持系统。极简主义模型基于一组理想化的假设，旨在仅捕获系统最显着的特征。决策支持模型倾向于服务于大规模应用程序，旨在回答现实世界的政策问题，包括真实数据，并通过适当的验证测试以建立可信度。

### 3.2 Applications overview

> Troisi et al (2005) applied agent-based simulation to model molecular self- assembly. Agents consist of individual molecules, and agent behaviours consist of the physical laws of molecular interaction. Such agent-based modeling approaches have found use in investigating pattern formation in the self- assembly of nano-materials, in explaining self-organized patterns formed in granular materials, and other areas.

Troisi等人（2005）应用基于智能体的模拟来模拟分子自组装。智能体由单个分子组成，智能体行为由分子相互作用的物理定律组成。这种基于智能体的建模方法已用于研究纳米材料自组装中的图案形成、解释颗粒材料中形成的自组织图案以及其他领域。

> In the biological sciences, agent-based modeling is used to model cell behaviour and interaction, the workings of the immune system, tissue growth, and disease processes. Generally, authors contend that agent-based modeling offers benefits beyond traditional modeling approaches for the problems studied and use the models as electronic laboratories as an adjunct to traditional laboratories. Cellular automata are a natural application for modeling cellular systems (Alber et al, 2003). One approach uses the cellular automata grid to model structures of stationary cells comprising a tissue matrix. Mobile cells consisting of pathogens and antibodies are agents that diffuse through and interact with tissue and other co-located mobile cells. The Basic Immune Simulator is built on a general agent-based framework to model the interactions between the cells of the innate and adaptive immune system (Folcik et al, 2007). Approaches for modeling the immune system have inspired several agent-based models of intrusion detection for computer networks (Azzedine et al, 2007) and modeling the development and spread of cancer (Preziosi, 2003). Emonet et al (2005) developed an agent- based simulator AgentCell for modeling the chemotaxis processes for motile behaviour of the E. Coli bacteria. In this multi-scale simulation, agents are modeled as individual molecules as well as whole cells. The model is used to study how the range of natural cell diversity at the molecular level is responsible for the observed range of cell movement behaviours.

在生物科学中，基于智能体的建模用于模拟细胞行为和相互作用、免疫系统的运作、组织生长和疾病过程。一般来说，作者认为，基于智能体的建模为所研究的问题提供了超越传统建模方法的好处，并将模型用作电子实验室作为传统实验室的辅助手段。元胞自动机是模拟元胞系统的自然应用（Alber等人，2003）。一种方法使用元胞自动机网格来模拟包含组织基质的静止细胞的结构。由病原体和抗体组成的移动细胞是通过组织和其他共位移动细胞扩散并相互作用的病原体。基本免疫模拟器建立在基于通用代理的框架之上，用于模拟先天免疫系统和适应性免疫系统细胞之间的相互作用（Folcik等人，2007）。免疫系统建模的方法启发了几种基于代理的计算机网络入侵检测模型（Azzedine等人，2007）和癌症发展和扩散建模（Preziosi，2003）。Emonet等人（2005）开发了一种基于智能体的模拟器AgentCell，用于模拟大肠杆菌运动行为的趋化过程。在这种多尺度模拟中，智能体被建模为单个分子和整个细胞。该模型用于研究分子水平上的自然细胞多样性范围如何导致观察到的细胞运动行为范围。
 
> In ecology, agent-based modeling is used to model diverse populations of individuals and their interactions. Mock and Testa (2007) develop an agent- based model of predator-prey relationships between transient killer whales and threatened marine mammal species (sea lions and sea otters) in Alaska. The authors state that until now only simplistic, static models of killer whale consumption had been constructed because of the fact that the interactions between transient killer whales and their marine mammal prey are poorly suited to classical predator-prey modeling approaches.

在生态学中，基于智能体的建模用于对不同的个体群体及其相互作用进行建模。Mock和Testa（2007）在阿拉斯加开发了一个基于代理的模型，用于观察短暂的虎鲸与受威胁的海洋哺乳动物物种（海狮和海獭）之间的捕食者-猎物关系。作者指出，到目前为止，由于瞬态虎鲸与其海洋哺乳动物猎物之间的相互作用不适合经典的捕食者-猎物建模方法，因此只构建了简单的静态虎鲸消费模型。

> Agent-based epidemic and pandemic models incorporate spatial and network topologies to model people’s realistic activity and contact patterns (Carley et al, 2006; Epstein et al, 2007). The focus is on understanding tipping point conditions that might lead to an epidemic and identifying possible mitigation measures. These models explicitly consider the role of people’s behaviour and interactions through social networks as they affect the spread of infectious diseases.

基于智能体的流行病和大流行模型结合了空间和网络拓扑来模拟人们的真实活动和接触模式（Carley 等人，2006 年;Epstein 等人，2007 年）。重点是了解可能导致流行病的临界点条件，并确定可能的缓解措施。这些模型明确考虑了人们通过社交网络的行为和互动的作用，因为它们会影响传染病的传播。

> Computational social science is an emerging field that combines modeling and simulation with the social science disciplines (Sallach and Macal, 2001). Agent-based models have been developed in the fields of economics, sociology, anthropology, and cognitive science. Various social phenomena have been investigated using agent-based models that are not easily modeled using other approaches (Macy and Willer, 2002; Gilbert and Troitzsch, 2005). Theore- tical applications include social emergence (Sawyer, 2005), the emergence of cooperation (Axelrod, 1997), the generation of social instability (Epstein, 2002), and the collective behaviour of people in crowds (Pan et al, 2007). Sakoda (1971) formulated one of the first social agent-based models, the Checkerboard Model, which relied on a cellular automaton. Using a similar approach, Schelling developed a model of housing segregation in which agents represent homeowners and neighbours, and agent interactions represent agents’ perceptions of their neighbours (Schelling, 1978). Schelling showed that housing segregation patterns can emerge that are not necessarily implied or consistent with the objectives of the individual agents. Epstein and Axtell (1996) extended the notion of modeling people to growing entire artificial societies through agent-based simulation in the grid-based Sugarscape model. Sugarscape agents emerged with a variety of characteristics and behaviours, highly suggestive of a realistic, although rudimentary and abstract, society. These early grid-based models with limited numbers of social agents are now being extended to large-scale simulations over realistic social spaces such as social networks and geographies through real-time linkages with GIS.

计算社会科学是一个新兴领域，它将建模和模拟与社会科学学科相结合（Sallach and Macal，2001）。在经济学、社会学、人类学和认知科学领域已经开发了基于智能体的模型。使用基于智能体的模型研究了各种社会现象，而这些模型不容易使用其他方法建模（Macy and Willer，2002;Gilbert 和 Troitzsch，2005 年）。理论应用包括社会涌现（Sawyer，2005）、合作的出现（Axelrod，1997）、社会不稳定的产生（Epstein，2002）以及人群中人们的集体行为（Pan et al，2007）。Sakoda（1971）制定了第一个基于社会代理的模型之一，即棋盘模型，该模型依赖于元胞自动机。使用类似的方法，谢林开发了一种住房隔离模型，其中代理人代表房主和邻居，代理人互动代表代理人对邻居的看法（谢林，1978）。谢林表明，住房隔离模式可能会出现，这些模式不一定暗示或与个体主体的目标一致。Epstein 和 Axtell （1996） 通过基于网格的 Sugarscape 模型中基于智能体的模拟，将人建模的概念扩展到整个人工社会的成长中。Sugarscape 代理人具有各种特征和行为，高度暗示了一个现实的、尽管是初级和抽象的社会。这些早期基于网格的模型具有有限数量的社交代理，现在正在通过与 GIS 的实时链接扩展到对现实社会空间（如社交网络和地理）的大规模模拟。

> In many economic models based on standard micro-economic theory, simplifying assumptions are made for analytical tractability. These assump- tions include (1) economic agents are rational, which implies that agents have well-defined objectives and are able to optimize their behaviour, (2) economic agents are homogeneous, that is, agents have identical characteristics and rules of behaviour, (3) the system experiences primarily decreasing returns to scale from economic processes (decreasing marginal utility, decreasing marginal productivity, etc), and (4) the long-run equilibrium state of the system is the primary information of interest. Agent-based modeling allows relaxing the standard assumptions of classical economics (Arthur et al, 1997) so the transient states that are encountered along the way to equilibrium can be investigated (Axtell, 2000). This interest has spawned the field of Agent-based Computational Economics (Tesfatsion, 2002; Tesfatsion and Judd, 2006). Much applicable work is being done on understanding how people make decisions in actual situations in such fields as behavioural economics and neuro-economics. This work offers promise in building better empirically based models of agent behaviours that consider rational factors and emotion.

在许多基于标准微观经济理论的经济模型中，对分析的可处理性进行了简化的假设。这些假设包括：（1）经济主体是理性的，这意味着主体具有明确的目标，并且能够优化其行为;（2）经济主体是同质的，即主体具有相同的特征和行为规则;（3）系统主要经历经济过程的规模回报递减（边际效用降低，边际生产率下降， 等），（4）系统的长期平衡状态是主要关注的信息。基于智能体的建模允许放宽经典经济学的标准假设（Arthur et al， 1997），因此可以研究在达到平衡的过程中遇到的瞬态（Axtell， 2000）。这种兴趣催生了基于智能体的计算经济学领域（Tesfatsion，2002;Tesfatsion 和 Judd，2006 年）。在行为经济学和神经经济学等领域，人们正在做许多适用的工作来理解人们在实际情况下如何做出决定。这项工作为建立更好的基于经验的代理行为模型提供了希望，这些模型考虑了理性因素和情感。

> Agent-based models are being used to analyze markets, both existing and hypothetical. Charania et al (2006) use agent-based simulation to model possible futures for a market in sub-orbital space tourism. Each agent is a representation of an entity within the space industry. Tourism companies seek to maximize profits while they compete with other companies for sales. Customers evaluate the products offered by the companies according to their individual tastes and preferences. López-Sánchez et al (2005) developed a multi-agent based simulation of news digital markets adapting traditional business models to investigate market dynamics. Yin (2007) developed an agent-based model of Rocky Mountain tourism applied to the town of Breckenridge, Colorado; the model was used to explore how homeowners’ investment and reinvestment decisions are influenced by the level of investment and amenities available in their neighbourhoods. Tonmukayakul (2007) developed an agent-based computational economics model to study market mechanisms for the secondary use of the radio spectrum. Using transaction cost economics as the theoretical framework, the model was used to identify the conditions for when and why the secondary use market could emerge and what form it might take.

基于智能体的模型被用于分析现有和假设的市场。Charania等人（2006）使用基于智能体的模拟来模拟亚轨道太空旅游市场的可能未来。每个代理都是航天工业中一个实体的代表。旅游公司寻求利润最大化，同时与其他公司竞争销售。客户根据个人口味和喜好评估公司提供的产品。López-Sánchez等人（2005）开发了一种基于多智能体的新闻数字市场模拟，采用传统的商业模式来研究市场动态。Yin（2007）开发了一种基于代理的落基山旅游模型，应用于科罗拉多州布雷肯里奇镇;该模型用于探索房主的投资和再投资决策如何受到其社区投资水平和便利设施的影响。Tonmukayakul（2007）开发了一种基于智能体的计算经济学模型，用于研究无线电频谱二次使用的市场机制。该模型以交易成本经济学为理论框架，用于确定二次使用市场何时以及为何会出现的条件以及它可能采取何种形式。

> Archaeology and anthropology are making use of large-scale agent-based modeling by providing an experimental virtual laboratory for long-vanished civilizations. Kohler et al (2005) employed large-scale agent-based simulations based on archaeological evidence to understand the social and cultural factors responsible for the disappearance of the ancient Pueblo in some parts of the south-western USA. Wilkinson et al (2007) used agent-based modeling to understand the growth and decline of ancient Mesopotamians.

考古学和人类学正在利用大规模的基于智能体的建模，为早已消失的文明提供实验性虚拟实验室。Kohler等人（2005）采用基于考古证据的大规模基于智能体的模拟来了解导致美国西南部某些地区古代普韦布洛人消失的社会和文化因素。Wilkinson等人（2007）使用基于智能体的建模来了解古代美索不达米亚人的成长和衰落。

> Agent-based models of many real-world systems tend to consist of a mix of physical components (modeled as agents) and social agents, termed ‘socio-technic’ systems. Examples of such systems for which large-scale agent- based models have been developed include traffic, air traffic control, military command and control and net-centric operations, physical infrastructures and markets, such as electric power and integrated energy markets. For example, Cirillo et al (2006) used an agent-based approach to model the Illinois electric power markets under conditions of deregulation in an effort to anticipate likely effects on electricity prices and reliability.

许多现实世界系统的基于智能体的模型往往由物理组件（建模为智能体）和社会智能体的混合组成，称为“社会技术”系统。已开发大规模代理模型的此类系统的例子包括交通、空中交通管制、军事指挥和控制以及以网络为中心的行动、有形基础设施和市场，如电力和综合能源市场。例如，Cirillo等人（2006）使用基于智能体的方法在放松管制的条件下对伊利诺伊州电力市场进行建模，以预测对电价和可靠性的可能影响。

> This special issue adds to the growing list of agent-based model applications. Qu et al use their model of egg plant growth to promote understanding of the interactions between plant architecture and physiological processes. Chen and Hardoon use their model to examine cell division and migration in the colonic crypt to better understand the mechanisms of tumorigenesis.

本期特刊增加了不断增长的基于智能体的模型应用程序列表。Qu等人使用他们的卵子植物生长模型来促进对植物结构和生理过程之间相互作用的理解。Chen和Hardoon使用他们的模型来检查结肠隐窝中的细胞分裂和迁移，以更好地了解肿瘤发生的机制。


## 4 Methods for agent-based modeling

### 4.1 Agent model design

> When developing an agent-based model, it is useful to ask a series of questions, the answers to which will lead to an initial model design:

在开发基于智能体的模型时，提出一系列问题很有用，这些问题的答案将导致初始模型设计：

> 1. What specific problem should be solved by the model? What specific questions should the model answer? What value-added would agent-based modeling bring to the problem that other modeling approaches cannot bring?

1. 模型应该解决什么具体问题？模型应回答哪些具体问题？基于智能体的建模会给其他建模方法带来什么附加值？

> 2. What should the agents be in the model? Who are the decision makers in the system? What are the entities that have behaviours? What data on agents are simply descriptive (static attributes)? What agent attributes would be calculated endogenously by the model and updated in the agents (dynamic attributes)?

2. 模型中的代理应该是什么？谁是系统中的决策者？有哪些实体有行为？代理上的哪些数据只是描述性的（静态属性）？哪些智能体属性将由模型内生计算并在智能体中更新（动态属性）？ 

> 3. What is the agents’ environment? How do the agents interact with the environment? Is an agent’s mobility through space an important consideration?

3. 代理的环境是什么？代理如何与环境交互？智能体在空间中的移动性是一个重要的考虑因素吗？

> 4. What agent behaviours are of interest? What decisions do the agents make? What behaviours are being acted upon? What actions are being taken by the agents?

4. 对哪些智能体行为感兴趣？代理做出什么决定？正在对哪些行为采取行动？代理正在采取哪些行动？

> 5. How do the agents interact with each other? With the environment? How expansive or focused are agent interactions?

5. 代理如何相互交互？与环境？座席互动的广度或集中度如何？

> 6. Where might the data come from, especially on agent behaviours, for such a model?

6. 对于这样的模型，数据可能来自哪里，尤其是关于代理行为的数据？

> 7. How might you validate the model, especially the agent behaviours?

7. 如何验证模型，尤其是代理行为？

> Answering these questions is an essential part of the agent-based model design process. There are a variety of approaches to designing and implementing agent-based models. North and Macal (2007) discuss both design methodol- ogies and selected implementation environments in depth. Marsh and Hill (2008) offer an initial methodology for defining agent behaviours in an application for unmanned autonomous vehicles. Overall, bottom-up, highly iterative design methodologies seem to be the most effective for practical model development. Modern software (and model) development practices dictate that model design be independent of model implementation. That is, a good software (model) design should be able to be implemented in whatever computer language or coding scheme is selected.

回答这些问题是基于智能体的模型设计过程的重要组成部分。有多种方法可以设计和实现基于智能体的模型。North和Macal（2007）深入讨论了设计方法和选定的实现环境。Marsh和Hill（2008）提供了一种初始方法，用于定义无人驾驶汽车应用中的代理行为。总体而言，自下而上、高度迭代的设计方法对于实际模型开发似乎是最有效的。现代软件（和模型）开发实践要求模型设计独立于模型实现。也就是说，一个好的软件（模型）设计应该能够用任何选择的计算机语言或编码方案来实现。 
 
>  The communication of a model, its design assumptions, and detailed elements is essential if models are to be understood and reused by others than their original developers. Grimm et al (2006) present a proposed standard protocol for describing agent-based and related models as a first step for establishing a more detailed common format.

如果要让模型被原始开发人员以外的其他人理解和重用，模型的通信、其设计假设和详细元素是必不可少的。Grimm等人（2006）提出了一种建议的标准协议，用于描述基于智能体和相关模型，作为建立更详细的通用格式的第一步。

### 4.2 Agent model implementation

> Agent-based modeling can be done using general, all-purpose software or programming languages, or it can be done using specially designed software and toolkits that address the special requirements of agent modeling. Agent modeling can be done in the small, on the desktop, or in the large, using large- scale computing cluster, or it can be done at any scale in-between these extremes. Projects often begin small, using one of the desktop ABMS tools, and then grow in stages into the larger-scale ABMS toolkits. Often one begins developing their first agent model using the approach that one is most familiar with, or the approach that one finds easiest to learn given their background and experience.

基于智能体的建模可以使用通用的通用软件或编程语言来完成，也可以使用专门设计的软件和工具包来完成，以满足智能体建模的特殊要求。代理建模可以在小型、桌面或大型中完成，使用大规模计算集群，也可以在这些极端之间的任何规模上完成。项目通常从小规模开始，使用桌面ABMS工具之一，然后分阶段发展到更大规模的ABMS工具包。通常，人们开始使用自己最熟悉的方法开发他们的第一个智能体模型，或者根据他们的背景和经验，人们认为最容易学习的方法。

> We can distinguish implementation alternatives to building agent-based models on the basis of the software used. Spreadsheets, such as Microsoft Excel, in many ways offer the simplest approach to modeling. It is easier to develop models with spreadsheets than with many of the other tools, but the resulting models generally allow limited agent diversity, restrict agent behaviours, and have poor scalability compared to the other approaches. Some macro-level programming is also needed using the VBA language.

我们可以根据所使用的软件来区分构建基于代理的模型的实现替代方案。电子表格（如 Microsoft Excel）在许多方面提供了最简单的建模方法。与许多其他工具相比，使用电子表格开发模型更容易，但与其他方法相比，生成的模型通常允许有限的代理多样性，限制代理行为，并且可扩展性较差。还需要使用 VBA 语言进行一些宏观级别的编程。

> General computational mathematics systems such as MATLAB and Mathematica, which many people may be already familiar with, can also be used quite successfully; however, these systems provide no specific capabilities for modeling agents. General programming languages such as Python, Java, and C++, and C also can be used, but development from scratch can be prohibitively expensive given that this would require the development of many of the available services already provided by specialized agent modeling tools. Most large-scale agent-based models use specialized tools, toolkits, or development environments based on reasons having to do with usability, ease of learning, cross-platform compatibility, and the need for sophisticated capabilities to connect to databases, graphical user interfaces and GIS.

很多人可能已经熟悉的通用计算数学系统，如MATLAB和Mathematica，也可以相当成功地使用;但是，这些系统没有为建模代理提供特定功能。也可以使用通用编程语言，如 Python、Java 和 C++，以及 C，但从头开始开发可能非常昂贵，因为这需要开发许多由专门的代理建模工具已经提供的可用服务。大多数基于智能体的大规模模型使用专用工具、工具包或开发环境，其原因与可用性、易学性、跨平台兼容性以及连接到数据库、图形用户界面和 GIS 的复杂功能需求有关。

### 4.3 Agent modeling services

> Regardless of the specific design methodology that is selected, a range of services is commonly required for implementing large-scale models that include real data and geo-spatial environments, which are becoming more prevalent. Some of the more common capabilities include project specification services; agent specification services; input data specification and storage services; model execution services; results storage and analysis services; and model packaging and distribution services.

无论选择哪种具体的设计方法，通常都需要一系列服务来实现包含真实数据和地理空间环境的大型模型，这些模型正变得越来越普遍。一些更常见的功能包括项目规范服务;代理规范服务;输入数据规范和存储服务;模型执行服务;结果存储和分析服务;以及模型包装和分销服务。

> Project specification services provide a way for modelers to identify which sets of resources (eg files) constitute each model. There are three common approaches, depending on how much support the implementation environ- ment provides for the modeler: (1) the library-oriented approach, (2) the integrated development environment (IDE) approach, and (3) the hybrid approach.

项目规范服务为建模者提供了一种方法来识别构成每个模型的资源集（例如文件）。根据实现环境为建模者提供的支持程度，有三种常见的方法：（1）面向库的方法，（2）集成开发环境（IDE）方法，以及（3）混合方法。

> In the library-oriented approach to project specification, the agent modeling tool consists of a library of routines organized into an application program- ming interface (API). Modelers create models by making a series of calls to the various functions within the modeling toolkit. It is the responsibility of modelers to ensure that the correct call sequences are used and that all of the required files are present. In exchange, modelers have great flexibility in the way that they define their models. Examples include the Java archives (JAR) used by Repast for Java (North et al, 2006; ROAD, 2009) or MASON (GMU, 2009); the binary libraries used by Swarm (SDG, 2009); and the Microsoft.NET assemblies used by Repast for the Microsoft.NET framework (North et al, 2006; ROAD, 2009).

在面向库的项目规范方法中，代理建模工具由一个例程库组成，这些例程被组织成一个应用程序编程接口（API）。建模者通过对建模工具包中的各种函数进行一系列调用来创建模型。建模者有责任确保使用正确的调用序列，并且存在所有必需的文件。作为交换，建模者在定义模型的方式上具有很大的灵活性。示例包括 Repast 用于 Java 的 Java 存档 （JAR）（North 等人，2006 年;ROAD，2009）或MASON（GMU，2009）;Swarm 使用的二进制库（SDG，2009）;以及 Repast 用于 Microsoft.NET 框架的 Microsoft.NET 程序集（North 等人，2006 年;ROAD，2009 年）。

> The IDE approach to project specification uses a code or model editing program to organize model construction. IDE’s also provide a built-in mechanism to compile or interpret and then execute models. There are several options including combined ‘one file’ IDEs, factored multiple-file IDEs, and hybrid approaches. Combined ‘one file’ IDEs use a single file to describe each model. An example is NetLogo (Wilensky, 1999; NetLogo, 2009). These systems are often quite easy to initially learn and use, but do not always scale well to larger and more complex models as compared to the other project specification approaches. The scalability issues include difficulties supporting team develop- ment, difficulties with editing increasingly large model files, and difficulties in organizing and reorganizing model code as it grows. Factored multiple-file IDEs use a set of files to describe each model. They usually include some type of built- in file manager along with the editor. Factored multiple-file IDEs can use either custom development environments which are specially built for a given agent platform; standards-based environments such as Eclipse (Eclipse Foundation, 2009), or a mixture of custom and standards-based environments. Support for features like team development (ie two or more modelers simultaneously creating a model), version control (ie automated tracking of code changes), and refactoring (ie automated tools for reorganizing code) helps to make these environments more powerful than typical combined ‘one file’ IDEs. In many cases, these environments require more knowledge to use than ‘one file’ IDEs but they also tend to scale more effectively. However, they may be less flexible than hybrid systems in the more extreme cases of model size and complexity.

项目规范的 IDE 方法使用代码或模型编辑程序来组织模型构建。IDE 还提供了一个内置机制来编译或解释然后执行模型。有多种选择，包括组合的“一个文件”IDE、分解的多文件 IDE 和混合方法。组合的“一个文件”IDE 使用单个文件来描述每个模型。一个例子是NetLogo（Wilensky，1999;NetLogo，2009 年）。这些系统通常非常容易初始学习和使用，但与其他项目规范方法相比，并不总是能很好地扩展到更大、更复杂的模型。可扩展性问题包括支持团队开发的困难、编辑越来越大的模型文件的困难，以及随着模型代码的增长而组织和重组模型代码的困难。分解的多文件 IDE 使用一组文件来描述每个模型。它们通常包括某种类型的内置文件管理器以及编辑器。分解多文件 IDE 可以使用专为给定代理平台构建的自定义开发环境;基于标准的环境，例如 Eclipse（Eclipse Foundation，2009），或自定义环境和基于标准环境的混合。对团队开发（即两个或多个建模者同时创建模型）、版本控制（即自动跟踪代码更改）和重构（即用于重新组织代码的自动化工具）等功能的支持有助于使这些环境比典型的组合“一个文件”IDE 更强大。在许多情况下，这些环境比“一个文件”IDE需要更多的知识才能使用，但它们也往往可以更有效地扩展。但是，在模型大小和复杂性的更极端情况下，它们可能不如混合系统灵活。

> The hybrid approach to project specification allows modelers to use the environment as either a stand-alone library or a factored multiple-file IDE. Examples include Repast Simphony (North et al, 2007; ROAD, 2009) and AnyLogic (XJ Technologies, 2009). In exchange for this added flexibility, these environments may require more knowledge to use than other types of IDEs but they also tend to scale the most effectively.

项目规范的混合方法允许建模者将环境用作独立库或分解的多文件 IDE。例子包括Repast Simphony（North等人，2007;ROAD，2009）和AnyLogic（XJ Technologies，2009）。为了换取这种增加的灵活性，这些环境可能比其他类型的 IDE 需要更多的知识才能使用，但它们也往往可以最有效地扩展。

> Agent specification services provide a means for modelers to define the attributes and behaviours of agents. These services can use general purpose languages such as C++ or Java; textual domain-specific languages (DSLs) such as Mathematica or MATLAB (Macal, 2004b); or visual DSLs such as the Repast Simphony flowchart shown in Figure 2.4. Along with or included in the language features, some implementation environments provide special support for features such as adaptation and learning (eg neural networks); optimization (eg genetic algorithms); social networks; geographical informa- tion systems (GIS); and systems dynamics.

代理规范服务为建模者提供了一种定义代理属性和行为的方法。这些服务可以使用通用语言，如 C++ 或 Java;文本领域特定语言（DSL），如Mathematica或MATLAB（Macal，2004b）;或可视化 DSL，如图 2.4 所示的 Repast Simphony 流程图。除了语言功能或包含在语言功能中外，一些实现环境还为适应和学习（例如神经网络）等功能提供特殊支持;优化（例如遗传算法）;社交网络;地理信息系统（GIS）;和系统动力学。


> Input data specification and storage services allow users to setup and save data that defines model runs. Input data setup can be done visually by pointing and clicking to create agents, by using custom programs to create agents in specified patterns, or by using external input data files in customized or standardized file formats. The standard storage formats can include extensible markup language (XML) files, spreadsheets, databases, or GIS files. Some systems also allow ‘checkpointing’, which is saving and restoring the current state of a model at any time during execution.

输入数据规范和存储服务允许用户设置和保存定义模型运行的数据。输入数据设置可以通过以下方式直观地完成：指向并单击以创建代理，使用自定义程序以指定模式创建代理，或者使用自定义或标准化文件格式的外部输入数据文件。标准存储格式可以包括可扩展标记语言 （XML） 文件、电子表格、数据库或 GIS 文件。一些系统还允许“检查点”，即在执行过程中随时保存和恢复模型的当前状态。

> Model execution services provide a means for model users to run and interact with simulations. Interactive execution can include viewing and modifying the attributes of agents (ie agent ‘probing’); displaying agents in two and three dimensions; and running models without visual displays to quickly generate data (ie ‘batch execution’). Batch execution can include the execution of multiple model runs on one local computer or on clusters of computers.

模型执行服务为模型用户提供了一种运行仿真并与之交互的方法。交互式执行可以包括查看和修改代理的属性（即代理“探测”）;在二维和三维中显示代理;以及运行没有视觉显示的模型以快速生成数据（即“批量执行”）。批处理执行可以包括在一台本地计算机或计算机群集上执行多个模型运行。
 
> Results storage and analysis services allow model users to conveniently examine the results of individual model runs or sets of runs. Major analysis mechanisms include visualization, data mining, statistics, and report genera- tion. Most implementation environments allow modelers to produce output text or binary files during execution, primarily using programming. These output files can then be manually read into separate external analysis tools. Some implementation environments such as Repast Simphony (North et al, 2007; ROAD, 2009) and AnyLogic (XJ Technologies, 2009) include either built- in analysis tools or point-and-click mechanisms to create output files and directly invoke external analysis tools.

结果存储和分析服务使模型用户能够方便地检查单个模型运行或运行组的结果。主要的分析机制包括可视化、数据挖掘、统计和报告生成。大多数实现环境允许建模者在执行期间生成输出文本或二进制文件，主要使用编程。然后，这些输出文件可以手动读入单独的外部分析工具中。一些实现环境，如Repast Simphony（North等人，2007;ROAD，2009）和AnyLogic（XJ Technologies，2009）包括内置分析工具或点击机制，用于创建输出文件并直接调用外部分析工具。

> Model packaging and distribution services allow modelers to disseminate completed models to end users. There are a range of methods for packaging models including embedded-platform packaging, IDE-based packaging, and stand-alone packaging. Once models are packaged there are several ways to distribute the results including file-based distribution, installer-based distribu- tion, and web-based execution. In principle, any of the distribution options can be used with any of the packaging approaches. Embedded-platform packaging places models within larger surrounding software systems. This kind of packaging is often used for models that are built using the library project specification approach. This approach usually requires substantial software development knowledge. IDE-based packaging occurs when a model is developed using the IDE project specification approach and is then disseminated by distributing copies of the IDE with the model inside. This approach usually allows users to examine and change the model when they receive it. It also sometimes requires greater skill on the user’s part compared to the other packaging approaches since IDEs can be somewhat complex. Stand- alone packaging binds a model into a program separate from the development environment that was used to create it. This new program, commonly called the ‘runtime version’ of the model, can be distributed to end users. This approach is usually the simplest for users who want to execute the model but not examine or change the code.

模型打包和分发服务允许建模者将完成的模型传播给最终用户。打包模型的方法多种多样，包括嵌入式平台打包、基于 IDE 的打包和独立打包。打包模型后，有几种方法可以分发结果，包括基于文件的分发、基于安装程序的分发和基于 Web 的执行。原则上，任何分发选项都可以与任何打包方法一起使用。嵌入式平台打包将模型放置在更大的周围软件系统中。这种打包通常用于使用库项目规范方法构建的模型。这种方法通常需要大量的软件开发知识。当使用 IDE 项目规范方法开发模型，然后通过分发包含模型的 IDE 副本来传播时，就会发生基于 IDE 的打包。这种方法通常允许用户在收到模型时检查和更改模型。与其他打包方法相比，它有时还需要用户更高的技能，因为 IDE 可能有些复杂。独立打包将模型绑定到与用于创建模型的开发环境分开的程序中。这个新程序通常称为模型的“运行时版本”，可以分发给最终用户。对于想要执行模型但不检查或更改代码的用户来说，这种方法通常是最简单的。

> File-based distribution places the files that constitute the model in a user accessible location such as a CD, DVD, file server, or website. These files can be individually accessed or distributed in a compressed or uncompressed archive. Installer-based distribution uses a custom program which copies the model onto the user’s computer and then configures it for execution. Installers usually have graphical wizard-based interfaces that make installation more reliable than for the other distribution approaches because of the ability of the installation software to automatically fix common configuration issues. Web- based execution embeds a packaged model into a web page for execution from within a browser. Web-based execution is differentiated from simply making raw files or an installer available from a website in that it requires models to execute from within a browser or browser plug-in rather than simply being downloaded and installed from an online source. Web-based execution is often the easiest and fastest distribution method for users. However, reliability can suffer because of the varying functionality of the wide range of browsers and browser plug-ins that are in common use today.

基于文件的分发将构成模型的文件放置在用户可访问的位置，例如 CD、DVD、文件服务器或网站。这些文件可以单独访问或分发在压缩或未压缩的存档中。基于安装程序的分发使用自定义程序，该程序将模型复制到用户的计算机上，然后对其进行配置以供执行。安装程序通常具有基于图形向导的界面，由于安装软件能够自动修复常见的配置问题，因此安装比其他分发方法更可靠。基于 Web 的执行将打包的模型嵌入到网页中，以便从浏览器中执行。基于 Web 的执行与简单地从网站提供原始文件或安装程序的区别在于，它要求模型从浏览器或浏览器插件中执行，而不是简单地从在线资源下载和安装。对于用户来说，基于 Web 的执行通常是最简单、最快捷的分发方法。但是，由于当今常用的各种浏览器和浏览器插件的功能各不相同，可靠性可能会受到影响。

> This section shows that there is a wide range of ways to implement agent- based models. When evaluating agent modeling tools, it should be noted that no one approach is universally better for all situations. Rather, different kinds of implementation approaches and environments have various strengths and weakness depending on the modeling questions of interest. Furthermore, it is common to use different tools during different stages of model development. For example, a modeler might start with a combined ‘one file’ IDE for initial model prototyping and then later transition to a factored multiple-file IDE as the model scales up in size and complexity. Therefore, the existing range of tools can best be thought of as a portfolio of options from which good selections can be made for each modeling question and stage.

本节介绍实现基于代理的模型的方法有很多种。在评估智能体建模工具时，应该注意的是，没有一种方法适用于所有情况。相反，不同类型的实现方法和环境具有不同的优势和劣势，具体取决于感兴趣的建模问题。此外，在模型开发的不同阶段使用不同的工具是很常见的。例如，建模者可能会从组合的“一个文件”IDE 开始进行初始模型原型设计，然后随着模型大小和复杂性的增加而过渡到分解的多文件 IDE。因此，可以将现有的工具范围视为一个选项组合，从中可以为每个建模问题和阶段做出良好的选择。

## 5 Summary and conclusions

> ABMS is a new approach to modeling systems comprised of autonomous, interacting agents. There are a growing number of agent-based applications in a variety of fields and disciplines. ABMS is particularly applicable when agent adaptation and emergence are important considerations. Many agent-based software and toolkits have been developed and are widely used. A combination of several synergistic factors is moving ABMS forward rapidly. These factors include the continuing development of specialized agent-based modeling methods and toolkits, the widespread application of agent-based modeling, the mounting collective experience of the agent-based modeling community, the recognition that behaviour is an important missing element in existing models, the increasing availability of micro-data to support agent-based models, and advances in computer performance. Taken together, these factors suggest that ABMS promises to have far-reaching effects into the future on how businesses use computers to support decision-making, government uses models to make and support policy, and researchers use electronic laboratories to further their research.

ABMS是一种对由自主交互代理组成的系统进行建模的新方法。在各个领域和学科中，有越来越多的基于智能体的应用程序。当代理适应和出现是重要的考虑因素时，ABMS 特别适用。许多基于代理的软件和工具包已经开发并被广泛使用。几个协同因素的结合正在推动ABMS迅速向前发展。这些因素包括基于智能体的专业建模方法和工具包的持续发展、基于智能体的建模的广泛应用、基于智能体的建模社区的集体经验的增加、对行为是现有模型中重要缺失元素的认识、支持基于智能体的模型的微观数据的可用性增加，以及计算机性能的进步。综上所述，这些因素表明，ABMS有望在未来对企业如何使用计算机来支持决策、政府使用模型来制定和支持政策以及研究人员使用电子实验室来推进他们的研究产生深远的影响。