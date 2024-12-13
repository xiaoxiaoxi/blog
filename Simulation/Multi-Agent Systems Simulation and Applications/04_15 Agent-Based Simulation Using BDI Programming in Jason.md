# Chapter 15 Agent-Based Simulation Using BDI Programming in Jason

---

## 15.1 Introduction

> Programming languages for multi-agent system have received enormous research attention
in the last few years. Such languages are now very expressive yet with practical interpreters
and reasonably user-friendly platforms for developing multi-agent systems based on such
languages. One advantage of these languages for developing multi-agent systems is that
the language provides constructs for several concepts and abstractions used in designing or
specifying sophisticated multi-agent systems. So not only are these languages suitable for
implementing designs created with agent-oriented software engineering methodologies, but
they are also ideal for developing simulations with cognitive agents. In particular, the use
of such languages gives a direct declarative representation for an agent’s mental states, for
example the beliefs it currently holds about its environment or other agents sharing the
environment (e.g., in a particular simulation) or the goals it is currently trying to achieve,
as well as how the agent has decided to act upon the environment so as to bring about
those goals. As a consequence, human observers of a simulation developed with an agent
programming language can check not only how social phenomena emerge but also what
are the agents’ mental attitudes that emerged at the same time or led to the observed
social phenomena. This is of fundamental importance for future trends in social simulation
aiming at investigating the micro-macro link problem; that is, how social interaction and
organizations affect mental states and vice-versa.

用于多智能体系统的编程语言在过去几年中受到了巨大的研究关注。这些语言现在具有很强的表现力，
但具有实用的解释器和相当用户友好的平台，用于开发基于这些语言的多代理系统。这些语言用于开发多代理系统的一个优点是，
该语言为设计或指定复杂的多代理系统时使用的多个概念和抽象提供了构造。因此，这些语言不仅适合实现使用面向智能体的
软件工程方法创建的设计，而且还非常适合使用认知智能体开发模拟。特别是，使用此类语言为代理的心理状态提供了直接的陈述性表示，
例如它当前对其环境或其他共享环境的代理的信念（例如，在特定的模拟中）或它当前试图实现的目标，
以及代理如何决定对环境采取行动以实现这些目标。因此，使用代理编程语言开发的模拟的人类观察者
不仅可以检查社会现象是如何出现的，还可以检查同时出现或导致观察到的社会现象的代理的心理态度是什么。
这对于旨在研究微观-宏观链接问题的社会模拟的未来趋势具有根本意义;也就是说，社会互动和组织如何影响心理状态，反之亦然。

> Most available platforms for agent-based simulation offer easy to use interfaces so that
scientists can develop agent-based simulation even without much knowledge of programming. 
However, the consequence is that agents developed with those tools are either reactive 
or have very simple behavior. The main contribution of our approach (described in
this chapter) is that it supports the development of agent-based simulations where agents
are potentially much more sophisticated then typically used in current simulations. At the
same time, the use of efficient interpreters for agent programming languages means they
can run in reasonable time, unlike some AI-based approaches where there is, for example,
reasoning from first principles. Although this approach has not been tried extensively yet
for social simulation, it offers a completely new approach for developing agent-based simulations 
where agents have declarative representations of mental attitudes and display rational,
goal-directed behavior.

大多数可用的基于智能体的仿真平台都提供了易于使用的界面，因此即使没有太多的编程知识，科学家也可以开发基于智能体的仿真。
然而，结果是使用这些工具开发的代理要么是反应性的，要么具有非常简单的行为。我们的方法（在本章中描述）
的主要贡献是它支持基于代理的模拟的开发，其中代理可能比当前模拟中通常使用的要复杂得多。同时，使用代理编程语言的
高效解释器意味着它们可以在合理的时间内运行，这与一些基于 AI 的方法不同，例如，需要根据第一原理进行推理。
尽管这种方法尚未在社交模拟中得到广泛尝试，但它为开发基于代理的模拟提供了一种全新的方法，
其中代理具有心理态度的声明性表示，并表现出理性的、目标导向的行为。

> In this chapter, we will concentrate in introducing particularly the use of the Jason agent
platform for (social) simulation. Jason includes an interpreter for an extended version of
the AgentSpeak programming language, which is based on the BDI agent architecture. We
will first summarize the main characteristics of BDI agents and how they are implemented
in Jason and then discuss in detail some of the aspects which are particularly important for
simulation, for example the execution mode where agents can run synchronously (whereas
agents typically run asynchronously, reacting to perceived events by executing plans that
include the achievement of long-term goals), the support for developing environments where
agents are situated, Jason’s “mind inspector”, and the integration with code written in
traditional programming languages. We will also describe various ongoing projects which
aim to add various functionalities to the Jason platform; these in turn will have a significant
impact in the types of simulations that can be developed with Jason. The chapter also
has a running example showing how the various aspects of the platforms could be used in
(social) simulations.

在本章中，我们将重点介绍 Jason 代理平台在（社交）模拟中的使用。Jason 包括一个用于 AgentSpeak 
编程语言扩展版本的解释器，该语言基于 BDI 代理体系结构。我们将首先总结 BDI 代理的主要特征以及它们如何在 Jason 中实现，
然后详细讨论一些对模拟特别重要的方面，例如代理可以同步运行的执行模式（而代理通常异步运行，通过执行包括实现长期目标的
计划来对感知事件做出反应）， 支持开发代理所在的环境、Jason 的“Mind Inspector”，以及与用传统编程语言编写的代码的集成。
我们还将介绍各种正在进行的项目，这些项目旨在为 Jason 平台添加各种功能;这些反过来又会对 Jason 可以开发的模拟类型
产生重大影响。本章还有一个运行示例，展示了如何在（社交）模拟中使用平台的各个方面。

## 15.2 Programming Languages for Multi-Agent Systems

> In recent years, there has been an extremely rapid increase in the amount of research being
done on agent-oriented programming languages, and multi-agent systems techniques that
can be used in the context of an agent programming language. The number and range of
different programming language, tools, and platforms for multi-agent systems that have
appeared in the literature [Bordini et al., 2006] is quite impressive, in particular logic-
based languages [Fisher et al., 2007]. In [Bordini et al., 2005b], some of the languages that
have working interpreters of practical use were presented in reasonable detail. Other languages 
have been discussed in other available surveys, e.g. [Mascardi et al., 2004; Dastani
and Gomez-Sanz, 2006]. Even though we here do not discuss existing agent languages and
platforms, it is worth giving references to some examples of well known agent-oriented
programming and platforms: 3APL [Dastani et al., 2005] (and its recent 2APL variation),
MetateM [Fisher, 2004], ConGolog [de Giacomo et al., 2000], CLAIM [El Fallah Seghrouchni
and Suna, 2005], IMPACT [Dix and Zhang, 2005], Jadex [Pokahr et al., 2005], JADE 
[Bellifemine et al., 2005], SPARK [Morley and Myers, 2004], MINERVA [Leite et al., 2002],
SOCS [Alberti et al., 2005; Toni, 2006], Go! [Clark and McCabe, 2004], STEAM [Tambe,
1997], STAPLE [Kumar et al., 2002], JACK [Winikoff, 2005].

近年来，对面向代理的编程语言和可在代理编程语言上下文中使用的多代理系统技术的研究数量急剧增加。
文献中出现的用于多智能体系统的不同编程语言、工具和平台的数量和范围[Bordini et al.， 2006]令人印象深刻，
特别是基于逻辑的语言[Fisher et al.， 2007]。在 [Bordini et al.， 2005b] 中，
一些具有实际使用的有效解释器的语言被合理地详细地介绍。其他语言在其他可用的调查中已经讨论过，
例如 [Mascardi et al.， 2004;Dastani 和 Gomez-Sanz，2006 年]。尽管我们在这里不讨论现有的代理语言和平台，
但值得参考一些众所周知的面向代理的编程和平台的例子：
- 3APL [Dastani et al.， 2005]（及其最近的 2APL 变体）、
- MetateM [Fisher， 2004]、
- ConGolog [de Giacomo et al.， 2000]、
- CLAIM [El Fallah Seghrouchni 和 Suna， 2005]、
- IMPACT [Dix 和 Zhang， 2005]]、
- Jadex [Pokahr et al.， 2005]、
- JADE [Bellifemine et al.， 2005]、
- SPARK [Morley and Myers， 2004]、
- MINERVA [Leite et al.， 2002]、
- SOCS [Alberti et al.， 2005;Toni，2006 年]，
- Go！[Clark 和 McCabe，2004]、
- STEAM [Tambe，1997]、
- STAPLE [Kumar 等人，2002]、
- JACK [Winikoff，2005]。

> Quite a few of these languages are based on the BDI agent architecture or at least on the
essential notion of goal. Explicit representations of long-term goals that the agent is trying
to achieve are a fundamental requirement for the implementation of a software entity that
displays the kind of behavior that we expect of an “autonomous agent” [Wooldridge, 2002].
It allows agents to take further action when a plan executed to achieve a particular goal
fails to do so (e.g., because the environment where the agent is situated is unpredictable);
it also allows agents to reconsider the goals they committed themselves to achieve if new
opportunities are perceived in the changing environment. For this reason, it seems that,
at least conceptually, agent programming languages subsume the kind of reactive agent
behavior: we can write plans telling an agent how to behave in reaction to something
directly perceived in the environment, but we can also keep track of long-term goals the
agent is trying to achieve, and we can then add mechanisms to help the agent make decisions
on how to balance both types of behavior. On the other hand, reactive agent approaches
rely significantly on aspects of the environments as well as agent behavior; we mention in
Section 15.4.1 that existing approaches for environment modeling can be combined with
Jason, and indeed with other agent languages too (see, e.g., [Ricci et al., 2008]).

这些语言中有相当多基于 BDI 代理体系结构，或者至少基于 goal 的基本概念。
代理者试图实现的长期目标的明确表示是实现软件实体的基本要求，
该软件实体显示我们期望的“自主代理”的行为类型 [Wooldridge， 2002]。
它允许代理在为实现特定目标而执行的计划未能做到这一点时采取进一步的行动（例如，因为代理所在的环境是不可预测的）;
它还允许座席在不断变化的环境中发现新的机会时重新考虑他们承诺实现的目标。
出于这个原因，至少在概念上，代理编程语言似乎包含了反应式代理行为的类型：
我们可以编写计划告诉代理如何对环境中直接感知到的事物做出反应，但我们也可以跟踪代理试图实现的长期目标，
然后我们可以添加机制来帮助代理决定如何平衡这两种类型的行为。
另一方面，反应式代理方法在很大程度上依赖于环境的各个方面以及代理行为;
我们在第 15.4.1 节中提到，现有的环境建模方法可以与 Jason 结合使用，
实际上也可以与其他代理语言结合使用（参见 [Ricci et al.， 2008]）。

> However, it is important to bear in mind that these are just programming languages, they
do not provide any “intelligence” for free. What they do provide are abstractions which help
humans cope with the development of sophisticated (distributed) systems. Most multi-agent
programming platforms will work on top of agent-based middleware (e.g., JADE [Bellifemine
et al., 2005]) that make certain issues of distributed computing fairly transparent for 
developers. Another essential characteristic is that they provide direct mechanisms for agents
to act within an environment, and inter-agent communication uses much higher-level abstractions 
than in classical distributed systems: agents will typically use knowledge-level
communication languages, based on speech-act theory [Austin, 1975] (possibly changing
their mental states as a consequence). The other essential features of agent platforms and
languages are typically related to agents’ mental attitudes. An important aspect in this 
approach to distributed systems is that agents’ mental attitudes are private: no other software
component can directly access the current mental state of an agent.

但是，重要的是要记住，这些只是编程语言，它们并不免费提供任何“智能”。
它们提供的是抽象，可以帮助人类应对复杂（分布式）系统的开发。
大多数多代理编程平台将工作在基于代理的中间件（例如，JADE [Bellifemine et al.， 2005]）之上，
这使得分布式计算的某些问题对开发人员相当透明。另一个基本特征是它们为代理提供了在环境中行动的直接机制，
并且代理间通信使用比经典分布式系统高得多的抽象：代理通常会使用基于言语行为理论的知识级通信语言 
[Austin， 1975]（可能因此改变他们的心理状态）。代理平台和语言的其他基本特征通常与代理的心理态度有关。
这种分布式系统方法的一个重要方面是代理的心理态度是私密的：没有其他软件组件可以直接访问代理的当前心理状态。

### 15.3.1 Language




