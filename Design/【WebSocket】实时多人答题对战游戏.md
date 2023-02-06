# 【WebSocket】实时多人答题对战游戏

2019-09-10阅读 1.7K0

**前言**

**前两章教程，我们使用WebSocket的基础特性打造了一个小小聊天室，并在第二章对其进行了集群化改造。**

**系列教程回顾：**

[手把手搭建WebSocket多人在线聊天室](https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247485578&idx=1&sn=eac39f010b8c2be949e0daae770fd7ae&chksm=ebd7498bdca0c09d2dad0af154f53d2aa2c9a0cce6602d1814346257f74583ab5b7fbd2b7eb9&token=1203617022&lang=zh_CN&scene=21#wechat_redirect)

[【多人聊天室】WebSocket集群/分布式改造](https://mp.weixin.qq.com/s?__biz=MzI4Njg5MDA5NA==&mid=2247485578&idx=2&sn=2a5f586c680fb83a9472322c53c74e72&chksm=ebd7498bdca0c09dd53af942592fa50642d766c3363a01abbb134f42999932f40ad171cae9e5&token=1203617022&lang=zh_CN&scene=21#wechat_redirect)

**在本文中，我将介绍如何使用WebSocket向实时多人答题对战游戏提供服务端，并详细介绍通接口的设计。** 

这是我在最近作业竞赛中设计的小项目，和小伙伴们一起设计了整个游戏流程和后端代码，前端页面暂时就不放开给大家了，大家可以参考前两章教程自己动手写一下前端页面。

**本文内容摘要：**

- 在线游戏常用的通讯方案
- 如何使用WebSocket实现游戏对战实时通信
- 游戏步骤的画面演示和对应的WebSocket接口设计

**本文源码：**（妈妈再也不用担心我无法复现文章代码啦）

https://github.com/qqxx6661/websocket-game-demo

# **正文**

## **WebSocket实现在线多人游戏——对战答题**

### **在线游戏常用的通讯方案**

参考：

https://blog.csdn.net/honey199396/article/details/54603860

#### **HTTP**

> 优点：协议较成熟，应用广泛、基于TCP/IP，拥有TCP优点、研发成本很低，开发快速、开源软件较多，nginx,apache,tomact等 缺点：无状态无连接、只有PULL模式，不支持PUSH、数据报文较大 特性：基于TCP/IP应用层协议、无状态，无连接、支持C/S模式、适用于文本传输

#### **TCP**

> 优点：可靠性 、全双工协议、开源支持多、应用较广泛、面向连接、研发成本低、报文内容不限制（IP层自动分包，重传，不大于1452bytes） 缺点：操作系统：较耗内存，支持连接数有限、设计：协议较复杂，自定义应用层协议、网络：网络差情况下延迟较高、传输：效率低于UDP协议 特性：面向连接、可靠性、全双工协议、基于IP层、OSI参考模型位于传输层、适用于二进制传输

#### **WebScoket**

> 优点：协议较成熟、基于TCP/IP，拥有TCP优点、数据报文较小，包头非常小、面向连接，有状态协议、开源较多，开发较快 缺点： 特性：有状态，面向连接、数据报头较小、适用于WEB3.0，以及其他即时联网通讯

#### **UDP**

> 优点：操作系统：并发高，内存消耗较低、传输：效率高，网络延迟低、传输模型简单，研发成本低 缺点：协议不可靠、单向协议、开源支持少、报文内容有限，不能大于1464bytes、设计：协议设计较复杂、网络：网络差，而且丢数据报文 特性：无连接，不可靠，基于IP协议层，OSI参考模型位于传输层，最大努力交付，适用于二进制传输

#### **总结**

- 对于弱联网类游戏，必须消除类的，卡牌类的，可以直接HTTP协议，考虑安全的话直接HTTPS，或者对内容体做对称加密；
- 对于实时性，交互性要求较高，可以优先选择Websocket，其次TCP协议；
- 对于实时性要求极高，且可达性要求一般可以选择UDP协议；
- 局域网对战类，赛车类，直接来UDP协议吧；

### **WebSocket实现双人在线游戏实时通信**

我们采用websocket作为我们的通信方案，主要是因为我们希望对战双方能够实时显示对方的得分。

本小节详细介绍了我们在线问答对战游戏中，具体的websocket通讯方式定义。

**本问答游戏规则如下：**

- 用户打开h5页面后，输入自己的昵称，发送给服务端，服务端将用户昵称保存到hashmap，并记录用户状态（空闲，游戏中），接着用户进入大厅。
- 大厅中用户可以互相选择，一旦某用户选择了另一位用户，将触发开始游戏，双方进入答题模式。
- 答题的两位用户各回答10题，每题答对为10分，共100分，左上角页面显示自己的分数，右上角显示对方分数，实时通过websocket接收对方分数。
- 10题结束，双方等待对方总分，最后判断输赢，显示结果界面。

**所以我们需要设计三个WebSocket协议：**

- 用户创建昵称，进入玩家大厅
- 用户选择对手，双方进入游戏
- 对战过程实时显示双方分数

接下来详细介绍这三种WebSocket接口

#### **用户创建昵称，进入玩家大厅**

打开界面，进入游戏：

![img](https://ask.qcloudimg.com/http-save/yehe-1287328/cuijt0xjxx.png?imageView2/2/w/1620)

我们使用了HashMap存储用户状态，

```javascript
private Map<String, StatusEnum> userToStatus = new HashMap<>();
```

复制

用户状态分为空闲和游戏中：

```javascript
public enum StatusEnum {
    IDLE,
    IN_GAME
}
```

复制

WebSocket接口设计如下：

![img](https://ask.qcloudimg.com/http-save/yehe-1287328/xo371fwjcs.png?imageView2/2/w/1620)

WebSocket接口代码如下：

```javascript
@MessageMapping("/game.add_user")
    @SendTo("/topic/game")
    public MessageReply addUser(@Payload ChatMessage chatMessage, SimpMessageHeaderAccessor headerAccessor) throws JsonProcessingException {
        MessageReply message = new MessageReply();
        String sender = chatMessage.getSender();
        ChatMessage result = new ChatMessage();
        result.setType(MessageTypeEnum.ADD_USER);
        result.setReceiver(Collections.singletonList(sender));
        if (userToStatus.containsKey(sender)) {
            message.setCode(201);
            message.setStatus("该用户名已存在");
            message.setChatMessage(result);
            log.warn("addUser[" + sender + "]: " + message.toString());
        } else {
            result.setContent(mapper.writeValueAsString(userToStatus.keySet().stream().filter(k -> userToStatus.get(k).equals(StatusEnum.IDLE)).toArray()));
            message.setCode(200);
            message.setStatus("成功");
            message.setChatMessage(result);
            userToStatus.put(sender, StatusEnum.IDLE);
            headerAccessor.getSessionAttributes().put("username",sender);
            log.warn("addUser[" + sender + "]: " + message.toString());
        }
        return message;
    }
```

复制

#### **用户选择对手，双方进入游戏**

在大厅中选择玩家，随后会进入对战：

![img](https://ask.qcloudimg.com/http-save/yehe-1287328/cfy4q32yb8.jpeg?imageView2/2/w/1620)

我们使用了HashMap存储了正在对战的用户，给双方配对。

```javascript
private Map<String, String> userToPlay = new HashMap<>();
```

复制

WebSocket接口设计如下：

![img](https://ask.qcloudimg.com/http-save/yehe-1287328/87yerd60k2.png?imageView2/2/w/1620)

WebSocket接口代码如下：

```javascript
@MessageMapping("/game.choose_user")
    @SendTo("/topic/game")
    public MessageReply chooseUser(@Payload ChatMessage chatMessage) throws JsonProcessingException {
        MessageReply message = new MessageReply();
        String receiver = chatMessage.getContent();
        String sender = chatMessage.getSender();
        ChatMessage result = new ChatMessage();
        result.setType(MessageTypeEnum.CHOOSE_USER);
        if (userToStatus.containsKey(receiver) && userToStatus.get(receiver).equals(StatusEnum.IDLE)) {
            List<QuestionRelayDTO> list=new ArrayList<>();
            questionService.getQuestions(limit).forEach(item->{
                QuestionRelayDTO relayDTO=new QuestionRelayDTO();
                relayDTO.setTopic_id(item.getId());
                relayDTO.setTopic_name(item.getQuestion());
                List<Answer> answers=new ArrayList<>();
                answers.add(new Answer(1,item.getId(),item.getOptionA(),item.getResult()==1?1:0));
                answers.add(new Answer(2,item.getId(),item.getOptionB(),item.getResult()==2?1:0));
                answers.add(new Answer(3,item.getId(),item.getOptionC(),item.getResult()==3?1:0));
                answers.add(new Answer(4,item.getId(),item.getOptionD(),item.getResult()==4?1:0));
                relayDTO.setTopic_answer(answers);
                list.add(relayDTO);
            });
            result.setContent(mapper.writeValueAsString(list));
            result.setReceiver(Arrays.asList(sender, receiver));
            message.setCode(200);
            message.setStatus("匹配成功");
            message.setChatMessage(result);
            userToStatus.put(receiver, StatusEnum.IN_GAME);
            userToStatus.put(sender, StatusEnum.IN_GAME);
            userToPlay.put(receiver,sender);
            userToPlay.put(sender,receiver);
            log.warn("chooseUser[" + sender + "," + receiver + "]: " + message.toString());
        } else {
            result.setContent(mapper.writeValueAsString(userToStatus.keySet().stream().filter(k -> userToStatus.get(k).equals(StatusEnum.IDLE)).toArray()));
            result.setReceiver(Collections.singletonList(sender));
            message.setCode(202);
            message.setStatus("该用户不存在或已在游戏中");
            message.setChatMessage(result);
            log.warn("chooseUser[" + sender + "]: " + message.toString());
        }
        return message;
    }
```

复制

#### **对战过程实时显示双方分数**

对战过程中的演示图：左边显示我方分数，右边显示对方分数

![img](https://ask.qcloudimg.com/http-save/yehe-1287328/zi37t4y30o.png?imageView2/2/w/1620)

WebSocket接口设计如下：

![img](https://ask.qcloudimg.com/http-save/yehe-1287328/94evcvax4j.png?imageView2/2/w/1620)

WebSocket接口代码如下：

```javascript
@MessageMapping("/game.do_exam")
    @SendTo("/topic/game")
    public MessageReply doExam(@Payload ChatMessage chatMessage) throws JsonProcessingException {
        MessageReply message = new MessageReply();
        String sender = chatMessage.getSender();
        String receiver = userToPlay.get(sender);
        ChatMessage result = new ChatMessage();
        result.setType(MessageTypeEnum.DO_EXAM);
        log.warn("userToStatus:" + mapper.writeValueAsString(userToStatus));
        if (userToStatus.containsKey(receiver) && userToStatus.get(receiver).equals(StatusEnum.IN_GAME)) {
            result.setContent(chatMessage.getContent());
            result.setSender(sender);
            result.setReceiver(Collections.singletonList(receiver));
            message.setCode(200);
            message.setStatus("成功");
            message.setChatMessage(result);
            log.warn("doExam[" + receiver + "]: " + message.toString());
        }else{
            result.setReceiver(Collections.singletonList(sender));
            message.setCode(203);
            message.setStatus("该用户不存在或已退出游戏");
            message.setChatMessage(result);
            log.warn("doExam[" + sender + "]: " + message.toString());
        }
        return message;
    }
```

复制

### **进一步**

这个只是个两天赶出来的Demo，当然里成品还有非常大的差距。这里有几个需要继续解决的事情：

- 实现自动匹配/排行榜
- WebSocket通讯优化：在某些地方使用点对点通讯，而非全部使用广播通讯。

> 我们可以使用convertAndSendToUser()方法，按照名字就可以判断出来，convertAndSendToUser()方法能够让我们给特定用户发送消息。 spring webscoket能识别带”/user”的订阅路径并做出处理，例如，如果浏览器客户端，订阅了’/user/topic/greetings’这条路径，

```javascript
stompClient.subscribe('/user/topic/greetings', function(data) {
    //...
});
```

复制

> 就会被spring websocket利用UserDestinationMessageHandler进行转化成”/topic/greetings-usererbgz2rq”,”usererbgz2rq”中，user是关键字，erbgz2rq是sessionid，这样子就把用户和订阅路径唯一的匹配起来了.

## **参考文献**

点对点通讯：

https://blog.csdn.net/yingxiake/article/details/51224569

# **总结**

我们在本文中实现了在线多人对战游戏的服务端WebSocket接口设计，进一步巩固了对WebSocket的基础和应用范围的理解。

本文工程源代码：

https://github.com/qqxx6661/websocket-game-demo