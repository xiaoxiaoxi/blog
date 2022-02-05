# 盘点 Flow : Activiti 如何使用命令模式执行流程

[AntBlack ![lv-3](https://lf3-cdn-tos.bytescm.com/obj/static/xitu_juejin_web/e108c685147dfe1fb03d4a37257fb417.svg)](https://juejin.cn/user/3790771822007822)

2021年06月20日 15:57 · 阅读 1389

关注

这是我参与更文挑战的第12天，活动详情查看： [更文挑战](https://juejin.cn/post/6967194882926444557?utm_campaign=30day&utm_medium=Ccenter&utm_source=20210528)

> **首先分享之前的所有文章 , 欢迎点赞收藏转发三连下次一定 >>>>** 😜😜😜
> **文章合集 :** 🎁 [juejin.cn/post/694164…](https://juejin.cn/post/6941642435189538824)
> **Github :** 👉 [github.com/black-ant](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fblack-ant)

## 一 . 前言

在深入 Activiti 的使用者 , 发现他对命令模式进行了很深入的使用 , 这里来看一下他是如何灵活使用该模式的 :

## 二 . 命令模式简述

**原理 :** 命令模式的原理在于发送者发送命令 , 执行者执行命令 ,传递者传递命令 , 命令描述执行的动作

> 角色成员 :

- **Command（抽象命令类）**：抽象命令类一般是一个抽象类或接口，在其中声明了用于执行请求的execute()等方法

- **ConcreteCommand（具体命令类）**：具体命令类是抽象命令类的子类，实现了在抽象命令类中声明的方法，它对应具体的接收者对象，将接收者对象的动作绑定其中

- Invoker（调用者）

  ：调用者即请求发送者，它通过命令对象来执行请求。

  - invoke 更像是一个传令兵 , 而不是调用者

- **Receiver（接收者）**：接收者执行与请求相关的操作，它具体实现对请求的业务处理。

**我们来看一个命令模式的简单 Demo** >> 👉

> **Step 1** : 构建 Command 接口

每个行为 (Command) 都会对应一个具体的 Command 对象 , 但是他们都会通过实现一个具体的 Command 接口来实现 , **对应整个流程中 ,中间对象都面向接口行为 ,而不会关心具体的实现类型**

```java
public interface Command {  
    // 每个具体的 Command 都应该实现该方法
    public void exe();  
}  
复制代码
```

> **Step 2** : 构建一个具体的 Command 实现类

Command 单元 , 该对象用于调用 具体的 Command 业务类

```java
public class MyCommand implements Command {  

    private Receiver receiver;  

    public MyCommand(Receiver receiver) {  
        this.receiver = receiver;  
    }  

    @Override  
    public void exe() {  
        receiver.action();  
    }  
}  

复制代码
```

> **Step 3** : 命令接收人执行具体的命令

准确来说 , 该对象不算在命令模式体系中 , 他是具体的的业务对象.

```java
public class Receiver {  
    public void action(){  
        System.out.println("command received!");  
    }  
}  

复制代码
```

> **Step 4 :** 代理器用于传递命令

总代理类 , 获取 Command 命令 , 进行判断并且调用

```java
public class Invoker {  

    private Command command;  

    public Invoker(Command command) {  
        this.command = command;  
    }  

    public void action(){  
        command.exe();  
    }  
}  
复制代码
```

> **Step End : 测试**

```java
public class Test {  

    public static void main(String[] args) {  
        Receiver receiver = new Receiver();  
        Command cmd = new MyCommand(receiver);  
        Invoker invoker = new Invoker(cmd);  
        invoker.action();  
    }  
}  

复制代码
```

## 三 . Activiti 中的命令模式

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5af7babb5e7144f5b3b3d4deedee6a7e~tplv-k3u1fbpfcp-watermark.awebp)

### 3.1 命令对象

Activiti 中的命令对象接口为 Command , 他有很多实现类 :

![Command-system.png](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b4477ee0d88b4f6391854a6bb62bf1a4~tplv-k3u1fbpfcp-watermark.awebp)

**PS:因为太多 , 这里仅仅展示了一部分 , 这些对象共同实现了 Command 接口**

```java
public interface Command<T> {
  T execute(CommandContext commandContext);
}
复制代码
```

> 还是以 DeleteTaskCmd 为例 :

### 3.2 Command 实现类

```java
public class DeleteTaskCmd implements Command<Void>, Serializable {

  public Void execute(CommandContext commandContext) {
    // 简单魔改 . 省略主要逻辑
    deleteTask(commandContext, taskId);
    return null;
  }

  protected void deleteTask(CommandContext commandContext, String taskId) {
    // 调用其他的业务类执行业务  
    commandContext.getTaskEntityManager().deleteTask(taskId, deleteReason, cascade, cancel);
  }
}
复制代码
```

### 3.3 CommandInvoker 执行Command 代理

该类是最后得分发器 , 通过该方法创建新线程执行 Command 命令

```java
public class CommandInvoker extends AbstractCommandInterceptor {

  private static final Logger logger = LoggerFactory.getLogger(CommandInvoker.class);

  @Override
  @SuppressWarnings("unchecked")
  public <T> T execute(final CommandConfig config, final Command<T> command) {
    final CommandContext commandContext = Context.getCommandContext();

    // 执行命令
    commandContext.getAgenda().planOperation(new Runnable() {
      @Override
      public void run() {
        commandContext.setResult(command.execute(commandContext));
      }
    });

    // 循环执行操作
    executeOperations(commandContext);

    // 最后，调用执行树更改监听器
    if (commandContext.hasInvolvedExecutions()) {
      Context.getAgenda().planExecuteInactiveBehaviorsOperation();
      executeOperations(commandContext);
    }

    // resultStack.pollLast() 获取结果
    return (T) commandContext.getResult();
  }

  protected void executeOperations(final CommandContext commandContext) {
    while (!commandContext.getAgenda().isEmpty()) {
      // 构建线程 , 并且调用 executeOperation 执行
      Runnable runnable = commandContext.getAgenda().getNextOperation();
      executeOperation(runnable);
    }
  }

  public void executeOperation(Runnable runnable) {
    if (runnable instanceof AbstractOperation) {
      AbstractOperation operation = (AbstractOperation) runnable;

      // 操作没有执行或者操作执行了一次，并且没有结束
      if (operation.getExecution() == null || !operation.getExecution().isEnded()) {
        runnable.run();
      }
    } else {
      runnable.run();
    }
  }

  @Override
  public CommandInterceptor getNext() {
    return null;
  }

  @Override
  public void setNext(CommandInterceptor next) {
    throw new UnsupportedOperationException("CommandInvoker must be the last interceptor in the chain");
  }

}
复制代码
```

**PS : CommandInvoke 整体数据**

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bfe46f6e6b11468f82b3a956988ed738~tplv-k3u1fbpfcp-watermark.awebp)

这里可以看到 , 实际上 Command 对象已经设置为了 DeleteTaskCmd , 下面看一下 Command 命令谁生成的

### 3.4 Command 的调用

以上基本上就能看出命令模式的主要成员就已经说清楚了 , 这里还补充一下 Command 的调用

- **Step1 :** C- ActivitiTaskRuntimeService # deleteTask
- **Step2 :** C- TaskRuntimeImpl # delete
- **Step3 :** C- TaskServiceImpl # deleteTask : **生成 Command 命令**
- **Step4 :** C- CommandExecutorImpl # execute : 核心方法 , 调用拦截器链
- **Step5 :** C- CommandContextInterceptor # execute : 命令容器执行 Command

> Step 3 : **在其中可以看到创建了 command 对象**

```java
public void deleteTask(String taskId, String deleteReason, boolean cancel) {
    commandExecutor.execute(new DeleteTaskCmd(taskId, deleteReason, false, cancel));
}
复制代码
```

> Step 5 : CommandContextInterceptor 处理 Command 消息体

```java
public class CommandContextInterceptor extends AbstractCommandInterceptor {
  
  private static final Logger log = LoggerFactory.getLogger(CommandContextInterceptor.class);

  // 工程类及配置对象
  protected CommandContextFactory commandContextFactory;
  protected ProcessEngineConfigurationImpl processEngineConfiguration;

  public CommandContextInterceptor() {
  }

  public CommandContextInterceptor(CommandContextFactory commandContextFactory, ProcessEngineConfigurationImpl processEngineConfiguration) {
    this.commandContextFactory = commandContextFactory;
    this.processEngineConfiguration = processEngineConfiguration;
  }

  public <T> T execute(CommandConfig config, Command<T> command) {
   
    CommandContext context = Context.getCommandContext();

    boolean contextReused = false;
    // 检查异常,事务可能处于回滚状态，并且会触发一些其他命令进行补偿
    if (!config.isContextReusePossible() || context == null || context.getException() != null) {
      context = commandContextFactory.createCommandContext(command);
    } else {
   
      contextReused = true;
      context.setReused(true);
    }

    try {
      
      // 将操作推到堆栈中 ( getStack(commandContextThreadLocal).push(commandContext);)
      Context.setCommandContext(context);
      Context.setProcessEngineConfiguration(processEngineConfiguration);
      if (processEngineConfiguration.getActiviti5CompatibilityHandler() != null) {
        Context.setActiviti5CompatibilityHandler(processEngineConfiguration.getActiviti5CompatibilityHandler());
      }
        
      // 执行操作  
      return next.execute(config, command);

    } catch (Throwable e) {

      context.exception(e);
      
    } finally {
      try {
        if (!contextReused) {
          // 关闭容器
          context.close();
        }
      } finally {
        
        // 同时移除相关数据
        Context.removeCommandContext();
        Context.removeProcessEngineConfiguration();
        Context.removeBpmnOverrideContext();
        Context.removeActiviti5CompatibilityHandler();
      }
    }

    return null;
  }
  
}  

复制代码
```

## 总结

**目的:** 达到命令的发出者和执行者之间解耦 , 实现请求和执行分开
**本质:** 一个请求对应于一个命令，将发出命令的责任和执行命令的责任分割开。每一个命令都是一个操作
**结果:** 由于引用了抽象类 , 请求发送者 , 具体的命令与请求接收者互相解耦

**最后总结一下使用命令模式对 Activiti 的好处 :**

- 在业务中 , 创建一个 command 命令
- 构建容器后 ,让 command 命令在其中流转
  - 对于容器 , 只需要关注命令的实现方法 , 不需要关系命令的内部逻辑
  - 发送者不需要知道中间发生了什么 , 也不需要关心性能处理
- 最后 , 命令代理类收到命令 (此时命令中包含让谁去执行)
  - 命令代理类叫来执行对象(对象的引用) ,让其执行
  - **实际上 ,此处可以通过反射来获得执行对象 , 这样命令才真的只是个命令**