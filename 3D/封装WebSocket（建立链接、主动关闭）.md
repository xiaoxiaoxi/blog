# [封装WebSocket（建立链接、主动关闭） ](https://www.cnblogs.com/songForU/p/12596029.html)

## 一、前言

　　近期项目里需做一个在线聊天功能，就想要在对话的时候建立socket链接。又因为聊天只是其中一个部分，在它外面还有一些全局的消息通知需要接收，因此也需要建立socket链接。在该项目里不仅一处用到了socket，就想着封装一个socket的，可以在项目里调用。

之前也用过一次websocket，但那次是直接用的socke.io，我也忘了这次为啥没有继续使用，对这个也一知半解，似懂非懂，先一点一点记起来。具体是介绍和解释就不写了，主要写几个帮助理解的部分。

## 二、HTML5 WebSocket

　　WebSocket 是 HTML5 开始提供的一种在单个 TCP 连接上进行全双工通讯的协议。

### 2.1、创建WebSocket 实例

　　WebSocket 对象作为一个构造函数，用于新建 WebSocket 实例。

```
 var Socket = new WebSocket(url,[protocol]);
```

　　以上代码用于创建 WebSocket 对象,其中的第一个参数 url, 即为指定连接的 URL。第二个参数 protocol 是可选的，指定了可接受的子协议。一般来说，大多没有具体要求的，就只用写url即可。

### 2.2 websocket属性

`  例如：var ws = new WebSocket('ws://1xx.xxx.xxx.xxx:8080/ws');`打印出创建的socket对象，内容如下，这些也正是wensocket的属性。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
　　binaryType: "blob"                    //返回websocket连接所传输二进制数据的类型，如果传输的是Blob类型的数据,则为"blob"，如果传输的是Arraybuffer类型的数据，则为"arraybuffer"
　　bufferedAmount: 0　　　　　　　　　　　　 //为只读属性，用于返回已经被send()方法放入队列中但还没有被发送到网络中的数据的字节数。
　　extensions: ""
　　onclose: ƒ ()　　　　　　　　　　　　　　　//连接关闭时触发
　　onerror: ƒ ()　　　　　　　　　　　　　　　//通信发生错误时触发
　　onmessage: ƒ (e)　　　　　　　　　　　　  //客户端接收服务端数据时触发,e为接受的数据对象
　　onopen: ƒ ()　　　　　　　　　　　　　　　 //连接建立时触发
　　protocol: ""　　　　　　　　　　　　　　　　 //用于返回服务器端选中的子协议的名字；这是一个在创建websocket对象时，在参数protocols中指定的字符串。
　　readyState: 1　　　　　　　　　　　　　　　 //返回值为当前websocket的链接状态
　　url: "ws://1xx.xxx.xxx.xxx:8080/ws"    //返回值为当构造函数创建WebSocket实例对象时URL的绝对路径。
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

所有属性讲解清单：https://developer.mozilla.org/en-US/docs/Web/API/WebSocket

###  2.3 websocket属性之readyState

　　readyState返回当前websocket的链接状态，共有4种。可根据具体项目的需求来利用此状态，写对应的需求。

```
CONNECTING：值为0，表示正在连接。
OPEN：      值为1，表示连接成功，可以通信了。
CLOSING：   值为2，表示连接正在关闭。
CLOSED：    值为3，表示连接已经关闭，或者打开连接失败。
```

###  2.4 websocket的方法

假定我们使用了上述代码创建的websocket对象，下面两个方法可以在任意socket事件中调用，根据自己项目需求而定。

#### 　　ws.send() ：使用连接发送数据，可以发送你想要发送的各种类型数据，如Blob对象、ArrayBuffer 对象、基本或复杂的数据类型等；

```
ws.send('消息');
//发送对象需要格式转换，接受数据同理
ws.send(JSON.stringify(data));
```

#### 　　ws.close() : 关闭连接，用户可以主动调取此方法，来关闭连接。

## 三、封装websocket

　　可在项目中定义一个socket.js文件，在需要建立socket的页面引入此js文件，即可在一个项目中创建多个socket连接。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
var webSocket = null;
var globalCallback = null;//定义外部接收数据的回调函数

//初始化websocket
function initWebSocket(url) {
  if ("WebSocket" in window) {
    webSocket = new WebSocket(url);//创建socket对象
    console.log(webSocket)
  } else {
    alert("该浏览器不支持websocket!");
  }
  //打开
  webSocket.onopen = function() {
    webSocketOpen();
  };
  //收信
  webSocket.onmessage = function(e) {
    webSocketOnMessage(e);
  };
  //关闭
  webSocket.onclose = function() {
    webSocketClose();
  };
  //连接发生错误的回调方法
  webSocket.onerror = function() {
    console.log("WebSocket连接发生错误");
  };
}

//连接socket建立时触发
function webSocketOpen() {
  if (e === "LOGIN") {
    const data = {
      type: "CONNECT",
      token: sessionStorage.getItem("token") || ""
    };
    sendSock(data, function() {});
  }
  console.log("WebSocket连接成功");
}

//客户端接收服务端数据时触发,e为接受的数据对象
function webSocketOnMessage(e) {
  const data = JSON.parse(e.data);//根据自己的需要对接收到的数据进行格式化
  globalCallback(data);//将data传给在外定义的接收数据的函数，至关重要。
  /*在此函数中还可以继续根据项目需求来写其他东西。 比如我的项目里需要根据接收的数据来判断用户登录是否失效了，此时需要关闭此连接，跳转到登录页去。*/
}

//发送数据
function webSocketSend(data) {
  webSocket.send(JSON.stringify(data));//在这里根据自己的需要转换数据格式
}

//关闭socket
function webSocketClose() {
  //因为我建立了多个socket，所以我需要知道我关闭的是哪一个socket，就做了一些判断。
  if (
    webSocket.readyState === 1 &&
    webSocket.url === "ws://1xx.xx.xx.xxx:8088/ws"
  ) {
    webSocket.close();//这句话是关键，之前我忘了写，一直没有真正的关闭socket
    console.log("对话连接已关闭");
  }
}


//在其他需要socket地方调用的函数，用来发送数据及接受数据
function sendSock(agentData, callback) {
  globalCallback = callback;//此callback为在其他地方调用时定义的接收socket数据的函数，此关重要。
  //下面的判断主要是考虑到socket连接可能中断或者其他的因素，可以重新发送此条消息。
  switch (webSocket.readyState) {
    //CONNECTING：值为0，表示正在连接。
    case webSocket.CONNECTING:
      setTimeout(function() {
        webSocketSend(agentData, callback);
      }, 1000);
      break;
    //OPEN：值为1，表示连接成功，可以通信了。
    case webSocket.OPEN:
      webSocketSend(agentData);
      break;
    //CLOSING：值为2，表示连接正在关闭。
    case webSocket.CLOSING:
      setTimeout(function() {
        webSocketSend(agentData, callback);
      }, 1000);
      break;
    //CLOSED：值为3，表示连接已经关闭，或者打开连接失败。
    case webSocket.CLOSED:
      // do something
      break;
    default:
      // this never happens
      break;
  }
}

//将初始化socket函数、发送（接收）数据的函数、关闭连接的函数export出去
export default {
  initWebSocket,
  webSocketClose,
  sendSock
};
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 四、使用此socketJs文件**（主要在vue项目中使用封装的socket）**

　　因为我项目里涉及多出页面需要使用socket，所以我将此文件在main.js中，将其定义在原型上，使其在每个 Vue 的实例中均可使用。不用单独在每个页面都引入一次。

#### 　　1、部分main.js代码

```
import socketApi from "./tool/socket";//找到封装的socket.js文件
Vue.prototype.socketApi = socketApi;//将其挂在原型上，这样 $socketApi就在所有的 Vue 实例中可用了。
```

#### 　　2、某一vue页面

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<template>
   <div>在此页面使用封装的socket</div>
</template>

<script>
  export default {
    name: "Message",
    data() {
      return {
        wsUrl: " ws://172.16.10.140:8088/ws",//定义socket连接地址
        wsType: "CONNECT"
      };
    },
    methods: {
      // 接收socket回调函数返回数据的方法
      getConfigResult(res) {
       console.log(res);//服务端返回的数据
      },
      websocketSend(data) {
        //data为要发送的数据，this.getConfigResult为回调函数，用于在此页面接收socket返回的数据。
        //至关重要！我一开始没写这个，就蒙了，咋才能到拿到回来的数据呢。
        this.socketApi.sendSock(data, this.getConfigResult);
      },
    },
    beforeRouteLeave(to, from, next) {
      //在离开此页面的时候主动关闭socket
      this.socketApi.webSocketClose();
      next();
    },
    
    created() {
      //建立socket连接
      this.socketApi.initWebSocket(this.wsUrl);
      //data为和后端商量好的数据格式
      const data = {
        type:this.wsType,
        msg: "说的话",
      };
      this.websocketSend(data);
    }
  };
</script>

<style lang="scss" scoped>
</style>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

## 五、遇到的问题

### 1、**websocket Failed to execute 'send' on 'WebSocket': Still in CONNECTING state**

 

　　一开始我只是初始化了socket，并没有发送消息过去。于是websocket 实例化后（我以为的建立成功了），就立马发送数据，就报了这个错误，说“正在连接”。其实我以为的建立成功是我看到了我在连接成功后的回调函数里打印的一句话：“WebSocket连接成功”，到底是什么正在连接还是连接成功我也不知道，所以需要在发送数据前，利用socket.readyState先判断此时的连接状态。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
function sendSock(agentData, callback) {
  globalCallback = callback;//此callback为在其他地方调用时定义的接收socket数据的函数，此关重要。
  
//此处先判断socket连接状态 

  switch (webSocket.readyState) {
    //CONNECTING：值为0，表示正在连接。
    case webSocket.CONNECTING:
      setTimeout(function() {
        webSocketSend(agentData, callback);
      }, 1000);
      break;
    //OPEN：值为1，表示连接成功，可以通信了。
    case webSocket.OPEN:
      webSocketSend(agentData);
      break;
    //CLOSING：值为2，表示连接正在关闭。
    case webSocket.CLOSING:
      setTimeout(function() {
        webSocketSend(agentData, callback);
      }, 1000);
      break;
    //CLOSED：值为3，表示连接已经关闭，或者打开连接失败。
    case webSocket.CLOSED:
      // do something
      break;
    default:
      // this never happens
      break;
  }
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

### 2、后端要求在建立连接的时候先发送一条数据，用于确定当前连接的状态

在此项目里，因为建立的socket需要有不同的连接用途，所以后端要在建立连接的时候给它发消息，确定建立socket，等此条消息发送完以后，再发送一条数据确定开始对话的状态。当时我在疑惑，我都socket还没建立，怎么给你发消息呢，我在什么时候发给你呢？

解决办法是在open函数里，发送一条消息过去。

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
function webSocketOpen() {
//在此次定义好需要传过去的数据，先发送一个数据过去，data为与后端协议的数据类型
    const data = {
      type: "CONNECT",
      token: sessionStorage.getItem("token") || ""
    };
    sendSock(data, function() {});//调用发送数据的函数
  console.log("WebSocket连接成功");
}
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

 

## 六、其他未考虑的地方

1、因为socket连接也会因为各种因素中断，所以有人写了“保活”：保活的原理-->心跳，前端每隔一段时间发送一段约定好的message给后端，后端收到后返回一段约定好的message给前端，如果多久没收到前端就调用重连方法进行重连。详见：https://www.jianshu.com/p/a4eacaf8de17

2、关于socket.io使用介绍，https://www.cnblogs.com/dreamsqin/p/12018866.html

 