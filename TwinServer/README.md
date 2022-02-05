# 写在前面
Twin Server 是自己研发的一款用来支撑 游戏 或者 DigitalTwin 的服务器，正在逐步的开发的过程中。该部分的所有内容都是自行设计和撰写，拥有无限版权，可以转载但是需要说明出处。

# Twin Server

## 关于Twin Server
Twin Server 是一款用Java实现的游戏或DigitalTwin服务器。

## 总体组成结构

### Server
采用Netty实现的TCP服务器基础架构，实现基本的长连接，并构建了一个基本的服务器ui

### Model
服务器内部对象

### Message
网络通讯协议包的封装

### mongo
采用mongo db 实现对象持久保存的封装


