# Activiti工作流框架学习笔记（一）之通用数据表详细介绍

2020-01-08阅读 4980

Activiti工作流引擎自带了一套[数据库](https://cloud.tencent.com/solution/database?from=10680)表，这里面有一个需要注意的地方：

低于5.6.4的[MySQL](https://cloud.tencent.com/product/cdb?from=10680)版本不支持时间戳或毫秒级的日期。更糟糕的是，某些版本在尝试创建此类列时将引发异常，而其他版本则不会。执行自动创建/升级时，引擎将在执行DDL时更改它。使用DDL文件方法时，既可以使用常规版本也可以使用其中带有mysql55的特殊文件（这适用于低于5.6.4的任何版本）。后一个文件将具有没有毫秒精度的列类型。

曾经在5.6.0版本做过试验，发现是无法自动生成23张表的，但在5.6.4版本以上便可，因此，最好保证mysql版本在5.6.4以上。

**一.数据库表名称说明**

Activiti的数据库表分5大部分，名称以ACT开头，第二部分是表用例的两个字符的标志，该用例与服务API的大致匹配：

![img](https://ask.qcloudimg.com/http-save/6853689/1zv25bne88.png?imageView2/2/w/1620)

**二.ACT_GE_ \*通用数据表**

通用数据表用于存放一些通用的数据，这些表本身不关心特定的流程或者业务，只用于存放这些业务或者流程所使用的资源。通用数据表有两个，分别是ACT_GE_BYTEARRAY与ACT_GE_PROPERTY,它们都是以ACT_GE_*开头的。

**2.1 ACT_GE_BYTEARRAY资源表**

表ACT_GE_BYTEARRAY资源表用于保存于流程引擎相关的资源，流程文件进行部署时，流程定义的图片以及XML文件等数据，都会转换成byte数组保存到这个表中。该表设计了一个byte字段，用来保存资源的内容，该表包含以下字段：

![img](https://ask.qcloudimg.com/http-save/6853689/vk65yeet1u.png?imageView2/2/w/1620)

 注：Activiti为了保证整个流程引擎表中所产生的数据主键在整个流程引擎中是唯一的，使用了一个DbIdGenerator类生成主键，该类中保存了下一条数据的ID值和当前ID块最后一个ID值。

**2.2 ACT_GE_PROPERTY属性表**

Activiti将全部的属性抽象为key-value对，每个属性都有名称和值。

![img](https://ask.qcloudimg.com/http-save/6853689/es1carcgqd.png?imageView2/2/w/1620)

注：在初始化流程数据库时，会默认加入3条属性数据：next.dbid、schema.history和schema.version。

next.dbid:属性值为1时，表示Activiti数据库表ID生成时，当前ID块最大值为1（即数据库里还没有任何数据）。前面也提到，流程引擎是使用一个DbIdGenerator类来生成主键的，该类保存了下一条数据的ID值和当前ID块的最后一个ID值，所谓ID块就是Activiti数据产生时ID值时，就会从1开始到101进行取值作为数据ID，那么该ID块的最大值为101。DbIdGenerator在产生数据ID时，会判断当前ID值是否大于101（ID块最大值）。如果大于，则请求重新生成一个ID块，那么此时属性中的next.dbid属性值将会为201。

schema.history：属性表示数据表结构的更新历史，例如——

![img](https://ask.qcloudimg.com/http-save/6853689/hv5z0kc0pk.png?imageView2/2/w/1620)

create(5.22.0.0)即表示使用了5.22版本的初始化脚本创建。

schema.version：表示当前Activiti数据结构的版本。

**三.ACT_RE_ \*流程存储表**

存储表名称以ACT_RE开头，RE是repository单词的前两个字母，流程使用存储表来保存流程定义和部署信息相关的数据。

**3.1.ACT_RE_DEPLOYMENT部署数据表**

在流程引擎中，一次部署可以添加多个资源，即可以有图片与XML之类的资源，这些资源数据会保存到资源表（ACT_GE_BTYEARRAY），剩余部署信息，则保存到部署表中，部署名为ACT_RE_DEPLOYMENT，包含以下三个字段：

![img](https://ask.qcloudimg.com/http-save/6853689/4lunb4l422.png?imageView2/2/w/1620)

 **3.2.ACT_RE_PROCDEF流程定义表**

Activiti在部署流程文件时（.bpmn或者.bpmn20.xml），其除了会将内容保存到资源表外，还会解析流程文件的内容，形成特定的流程定义数据，写入到流程定义表（ACT_RE_PROCDEF）中，该表包含了以下的字段：

![img](https://ask.qcloudimg.com/http-save/6853689/7me5861nvw.png?imageView2/2/w/1620)

注：该表的主键与其他数据表不同的是，ACT_RE_PROCDEF表的主键是组合主键，其值为流程定义的KEY_字段值加流程定义的VERSION_字段值再加ID生成器生成的ID值，其中这三个值以冒号为分隔符。例如，KEY_值为baoxiaoProcess，VERSION_值为1，ID生成器生成的ID值为722504，则该主键为baoxiaoProcess:1:722504，如以下截图所示：

![img](https://ask.qcloudimg.com/http-save/6853689/3vwpkak8dg.png?imageView2/2/w/1620)

 **四.ACT_ID_ \*身份数据表** 

Activiti的整个身份证数据模块，可以独立于流程引擎而存在，身份数据表并没有保存流程相关的数据以及关联，身份表名称使用ACT_ID关联，ID是单词identity的前两个字母。

**4.1.ACD_ID_USER用户表**

流程引擎用户的信息被保存在ACT_ID_USER表中，该表有以下字段：

![img](https://ask.qcloudimg.com/http-save/6853689/q4s8g4msqp.png?imageView2/2/w/1620)

 **4.2.ACD_ID_GROUP用户组表**

使用ACT_ID_GROUP表来保存用户组的数据，该表有以下几个字段：

![img](https://ask.qcloudimg.com/http-save/6853689/waqv8q01n.png?imageView2/2/w/1620)

 **4.3.ACD_ID_MEMBERSHIP关系表**

关系表用来描述用户表与用户组表的对应关系：

![img](https://ask.qcloudimg.com/http-save/6853689/nlym75rvs8.png?imageView2/2/w/1620)

 注：该表的两个字段均做了外键约束，写入该表的数据时，必须要有用户和用户组数据与之关联。

**五.ACT_RU_ \*运行时数据表**

运行时数据表用来保存流程在运行过程中所产生的数据，例如流程实例、执行流和任务等，以ACT_RU开头，RU是单词runtime的前两个字母。

**5.1.ACT_RU_EXECUTION流程实例表**

 流程启动后，会产生一个流程实例，同时产生相应的执行流，流程实例和执行流数据均被保存在ACT_RU_EXECUTION表中。如果一个流程实例只要一条执行流，那么该表中只产生一条数据，该数据既表示执行流，也表示流程实例。

![img](https://ask.qcloudimg.com/http-save/6853689/o7nxkuxrxj.png?imageView2/2/w/1620)

 **5.2.ACT_RU_TASK流程任务表**

流程在运行过程中所产生的任务数据保存在ACT_RU_TASK，字段如下：

![img](https://ask.qcloudimg.com/http-save/6853689/ftarqh0fzc.png?imageView2/2/w/1620)

 **5.3.ACT_RU_VARIABLE流程参数表** 

流程引擎提供了ACT_RU_VARIABLE表来存放流程中的参数，这类参数包括流程实例参数、执行流参数和任务参数，各参数可以有多种类型。

![img](https://ask.qcloudimg.com/http-save/6853689/ou9rv9v5xm.png?imageView2/2/w/1620)

 **5.4.ACT_RU_IDENTITYLINK流程与身份关系表**

 用户组与用户之间存在的关系，使用ACT_ID_MEMBERSHIP表保存。用户或者用户组与流程数据之间的关系，则使用ACT_RU_IDENTITYLINK表进行保存。

![img](https://ask.qcloudimg.com/http-save/6853689/bx5kmyc45n.png?imageView2/2/w/1620)

 **5.5.ACT_RU_JOB工作数据表**

  在流程执行的过程中，会有一些工作需要定时或者重复执行，这类工作数据被保存到ACT_RU_JOB表中。

![img](https://ask.qcloudimg.com/http-save/6853689/y1hw6r2d7y.png?imageView2/2/w/1620)

 **5.6.ACT_RU_EVENT_SUBSCR事件描述表**

如果流程到达某类事件节点，Activiti会往ACT_RU_EVENT_SUBSCR表中加入事件描述数据，这些事件描述数据将会决定流程事件的触发。

![img](https://ask.qcloudimg.com/http-save/6853689/7y368k11jy.png?imageView2/2/w/1620)

 **六.ACT_HI_ \*历史数据表**

历史数据表就像流程引擎的日志表。被操作过的流程元素，将会被记录到李四表中。历史表名称以ACT_HI开头，HI是单词history的前两个字母。

**6.1.ACT_HI_PROCINST流程实例表**

流程实例的历史数据会被保存到ACT_HI_PROCINST表中，只要流程启动，Activiti就会将流程实例的数据写入ACT_HI_PROCINST表中。除了基本的流程字段外，与运行时数据表不同的是，历史流程实例表还会记录流程的开始活动ID的、活动结束ID等信息。

![img](https://ask.qcloudimg.com/http-save/6853689/pyw0qfqju7.png?imageView2/2/w/1620)

 **6.2.ACT_HI_ACTINST历史行为表**

历史行为表会记录每一个流程活动的实例，一个 流程活动将会被记录成一条数据，例如，流程中有开始事件，用户任务，结束事件各一个，当流程结束后，该表就会产生3条历史行为数据。

![img](https://ask.qcloudimg.com/http-save/6853689/hefcwyayjb.png?imageView2/2/w/1620)

 **6.3.附件表ACT_HI_ATTACHMENT**

使用任务服务（TaskService）的API，可以添加附件，这些附件数据将会保存到ACT_HI_ATTACHMENT表中。

![img](https://ask.qcloudimg.com/http-save/6853689/sihwgrmyh9.png?imageView2/2/w/1620)

  **6.4.评论表ACT_HI_COMMENT**

可以专门存放审批过程中的评论数据。

![img](https://ask.qcloudimg.com/http-save/6853689/t1czf5uczh.png?imageView2/2/w/1620)

本文参与[腾讯云自媒体分享计划](https://cloud.tencent.com/developer/support-plan)，欢迎正在阅读的你也加入，一起分享。