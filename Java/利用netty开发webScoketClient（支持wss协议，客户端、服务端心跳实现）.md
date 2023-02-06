# 利用netty开发webScoketClient（支持wss协议，客户端、服务端心跳实现）

https://blog.csdn.net/qq_42875345/article/details/122128440?utm_medium=distribute.pc_relevant.none-task-blog-2~default~baidujs_baidulandingword~default-5-122128440-blog-99410216.pc_relevant_default&spm=1001.2101.3001.4242.4&utm_relevant_index=8



***

## 前言

> 最近在使用 netty这个框架来开发 webScoketClient用来获取一些流式的数据，之后咱家的前端采用长连接和咱保持联系，咱们后端就是一个中转站，既要编写一个webScoketServer供咱家的前端有奶喝，也要编写一个webScoketClient去挤奶，同时为了保证这个奶是澳大利亚纯装牛奶，还需要用巴氏消毒法对奶做一个品质管控。这样咱家的公司才能有希望做大做强，我才有肉吃。而这也是我为什么写下本文的原因
> 

## 题外话

话说 前端 不是可以通过new WebSocket(url)的方式创建长连接，继而获取流式数据的吗，那为什么前端能干的活要后端来插一脚呢？原因很简单，通过后端来实现webScoketClient可以对比数据做一些落库、过滤、校验…等一系列的操作，可以保证数据的安全性，如果项目后阶段需要版本的迭代，也比较好去扩展需求，当然对于引用一些安全性不是那么高的流式数据，比如说实时的天气信息，那么由前端来实现就够了，我想也没有哪个人吃饱了撑的来攻击这个网站吧，说了这么多下面开始介绍正文webScoketCllient 的几种实现方式吧

## webScoketClient实现方式一（jacva_webscoket）

如果是wss请求则添加wss支持，如果是其他请求则正常创建 WebSocketClient

```java
import org.java_websocket.client.DefaultSSLWebSocketClientFactory;
import org.java_websocket.client.WebSocketClient;
import org.java_websocket.drafts.Draft;

import javax.net.ssl.*;
import java.net.URI;
import java.security.SecureRandom;
import java.security.cert.X509Certificate;
import java.util.Map;

public abstract class WebScoketClientPlus extends WebSocketClient {
    public WebScoketClientPlus(URI serverURI, Draft draft, Map<String, String> headers, int connecttimeout) {
        super(serverURI, draft, headers, connecttimeout);
        /**
         * 如果url包含wss，添加wss协议支持
         */
        if (serverURI.toString().contains("wss://")) {
            trustAllHosts(this);
        }
    }

    /**
     * 扩展方法：目前不做扩展
     */
    public abstract void extendMethod();

    public static void trustAllHosts(WebScoketClientPlus appClient) {
        System.out.println("start...");
        TrustManager[] trustAllCerts = new TrustManager[]{new X509TrustManager() {
            public X509Certificate[] getAcceptedIssuers() {
                return new X509Certificate[0];
            }

            public void checkClientTrusted(X509Certificate[] arg0, String arg1) {
            }

            public void checkServerTrusted(X509Certificate[] arg0, String arg1) {
            }
        }};
        try {
            /**
             * 添加wss支持
             */
            SSLContext sc = SSLContext.getInstance("TLS");
            sc.init((KeyManager[]) null, trustAllCerts, new SecureRandom());
            appClient.setWebSocketFactory(new DefaultSSLWebSocketClientFactory(sc));
        } catch (Exception var3) {
            var3.printStackTrace();
        }
    }
}

```

## webScoketClient工具类

通过 WebScoketClientPlus 类（指定webScoket请求头等参数）创建WebSocketClient对象，继而进行连接，当接收到流式数据的时候 onMessage方法将会触发，在此我们可以编写自己的业务逻辑，下文的代码仅仅只是将接收到的 msg 进行打印了一遍而已。***注意 onMessage 触发的条件是：方法参数数据类型与要接收数据类型一致，如果不一致可能会造成接收不到数据的问题***。

```java
import lombok.Data;
import lombok.SneakyThrows;
import lombok.extern.slf4j.Slf4j;
import org.java_websocket.WebSocket.Role;
import org.java_websocket.drafts.Draft;
import org.java_websocket.drafts.Draft_17;
import org.java_websocket.handshake.ServerHandshake;
import org.springframework.stereotype.Component;

import java.net.URI;
import java.net.URISyntaxException;
import java.nio.ByteBuffer;
import java.nio.CharBuffer;
import java.nio.charset.CharacterCodingException;
import java.nio.charset.Charset;
import java.nio.charset.CharsetDecoder;
import java.util.HashMap;
import java.util.Map;
import java.util.concurrent.CountDownLatch;
@Slf4j
@Data
@Component
public class WebScoketUtil {
    public static WebScoketClientPlus getConnect(String url, CountDownLatch countDownLatch) throws URISyntaxException {
        Map<String, String> headers = new HashMap();
        /**
         * 指定webScoket的请求头信息
         */
        headers.put("Sec-WebSocket-Extensions", "permessage-deflate; client_max_window_bits");
        headers.put("Sec-WebSocket-Version", "13");
        headers.put("Connection", "Upgrade");
        headers.put("Upgrade", "websocket");
        headers.put("Accept-Encoding", "gzip, deflate, br");
        headers.put("Accept-Language", "zh-CN,zh;q=0.9");
        headers.put("Cache-Control", "no-cache");
        /**
         * 指定角色为客户端
         */
        Draft draft = new Draft_17();
        draft.setParseMode(Role.CLIENT);
        WebScoketClientPlus connect = new WebScoketClientPlus(new URI(url), draft, headers, 10) {


            @Override
            public void extendMethod() {
                System.err.println("extendMethod");
            }

            @SneakyThrows
            public void onClose(int arg0, String arg1, boolean arg2) {
                System.err.println("onClose");
            }

            public void onError(Exception arg0) {
                System.err.println("onError");
            }

            public void onMessage(String arg0) {
                System.out.println("String 消息：" + arg0);
            }

            public void onOpen(ServerHandshake arg0) {
                countDownLatch.countDown();
                System.out.println("onOpen：" + arg0);
            }

            public void onMessage(ByteBuffer bytes) {
                Charset charset = Charset.forName("UTF-8");
                CharsetDecoder decoder = charset.newDecoder();
                CharBuffer charBuffer = null;
                String received = "";
                try {
                    charBuffer = decoder.decode(bytes);
                } catch (CharacterCodingException e) {
                    e.printStackTrace();
                }
                bytes.flip();
                received = charBuffer.toString();
                System.out.println("接收到的流式数据：" + received);
            }
        };
        connect.connect();
        return connect;
    }
}

```

## 简单编写测试

```java
 	private static CountDownLatch countDownLatch = new CountDownLatch(1);

    public static void main(String[] args) throws URISyntaxException, InterruptedException {
        WebScoketClientPlus connect = WebScoketUtil.getConnect("wss://127.0.0.1:5000/v1/api/ws", countDownLatch);
        /**
         * 阻塞线程，直至onOpen的回调触发代表连接成功，才会放行
         */
        countDownLatch.await();
        connect.send("{\"userId\"=1}");
    }

```



***

## webScoketClient实现方式二（netty）

emm用netty实现这个稍微有点复杂。我们通过对 ChannelFuture 对象添加监听器进行监听，如果通道正常开启，则准备握手升级协议（根据url中的scheme确定升级协议的类型，目前支持wss），否则递归的进行重连。如果重连次数达到最大值，将不会进行重连了

```java
import io.netty.bootstrap.Bootstrap;
import io.netty.channel.*;
import io.netty.channel.nio.NioEventLoopGroup;
import io.netty.channel.socket.nio.NioSocketChannel;
import io.netty.handler.codec.http.DefaultHttpHeaders;
import io.netty.handler.codec.http.HttpHeaders;
import io.netty.handler.codec.http.websocketx.WebSocketClientHandshaker;
import io.netty.handler.codec.http.websocketx.WebSocketClientHandshakerFactory;
import io.netty.handler.codec.http.websocketx.WebSocketVersion;
import io.netty.handler.logging.LogLevel;
import io.netty.handler.logging.LoggingHandler;
import io.netty.handler.ssl.SslContext;
import io.netty.handler.ssl.SslContextBuilder;
import io.netty.handler.ssl.util.InsecureTrustManagerFactory;
import lombok.Data;
import lombok.SneakyThrows;

import javax.net.ssl.SSLException;
import java.net.URI;
import java.net.URISyntaxException;
import java.util.concurrent.CountDownLatch;
import java.util.concurrent.TimeUnit;

/**
 * 1、通道的开启：发送syn、ack数据包
 * 2、三次握手：通道是可靠的，你可以和我交流了
 */
@Data
public class WebSocketClient {
    private String uri;
    private CountDownLatch latch;
    private ClientInitializer clientInitializer;
    private SslContext sslCtx;
    private String host;
    private int port;
    private String scheme;
    private URI websocketURI;
    private String type;
    private String userId;
    private Bootstrap bootstrap;
    private Channel channel;
    int repeatConnectCount = 0;

    public WebSocketClient(String uri, String type, CountDownLatch latch) throws URISyntaxException {
        this.uri = uri;
        this.websocketURI = new URI(uri);
        this.host = websocketURI.getHost();
        this.port = websocketURI.getPort();
        this.scheme = websocketURI.getScheme();
        this.latch = latch;
        this.type = type;
        if ("wss".equals(scheme)) {
            //初始化SslContext，这个在wss协议升级的时候需要用到
            try {
                this.sslCtx = SslContextBuilder.forClient()
                        .trustManager(InsecureTrustManagerFactory.INSTANCE).build();
            } catch (SSLException e) {
                e.printStackTrace();
            }
        } else if ("ws".equals(scheme)) {
            this.sslCtx = null;
        }
        this.clientInitializer = new ClientInitializer(latch, host, port, sslCtx, type, WebSocketClient.this);
    }

    public void connect() {
        EventLoopGroup group = new NioEventLoopGroup(4);
        try {
            bootstrap = new Bootstrap();
            bootstrap.option(ChannelOption.SO_KEEPALIVE, true)
                    .option(ChannelOption.TCP_NODELAY, true)
                    .option(ChannelOption.SO_BACKLOG, 1024 * 1024 * 10)
                    .group(group)
                    .handler(new LoggingHandler(LogLevel.INFO))
                    .channel(NioSocketChannel.class)
                    .handler(clientInitializer);
          doConnect(null,10000);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }


    @SneakyThrows
    protected void doConnect(ChannelHandlerContext ctx, Integer count) {
        //重连次数每次加一
        repeatConnectCount++;
        if (repeatConnectCount > count) {
            if (null != ctx) {
                System.out.println("通道关闭、重连失败");
                ctx.channel().close();
                return;
            }
        }
        if (channel != null && channel.isActive()) {
            System.err.println("通道正常");
            return;
        }
        //建立HTTP连接
        ChannelFuture future = bootstrap.connect(host, port).addListener(new ChannelFutureListener() {
            public void operationComplete(ChannelFuture futureListener) throws Exception {
                if (futureListener.isSuccess()) {
                    channel = futureListener.channel();
                    //连接成功重置重连次数为0
                    repeatConnectCount = 0;
                    System.out.println("通道开启成功~");
                    HttpHeaders httpHeaders = new DefaultHttpHeaders();
                    WebSocketClientHandshaker webSocketClientHandshaker = WebSocketClientHandshakerFactory.newHandshaker(websocketURI, WebSocketVersion.V13, (String) null, true, httpHeaders);
                    WebSocketClientHandler handler = (WebSocketClientHandler) channel.pipeline().get("websocketHandler");
                    //升级为ws协议
                    System.err.println("开始升级http协议~准备开始握手");
                    webSocketClientHandshaker.handshake(channel);
                    handler.setHandshaker(webSocketClientHandshaker);
                } else {
                    futureListener.channel().eventLoop().schedule(new Runnable() {
                        @Override
                        public void run() {
                            System.err.println("重试开启通道~" + repeatConnectCount);
                            doConnect(ctx, count);
                        }
                    }, 3, TimeUnit.SECONDS);
                }
            }
        });
        channel = future.channel();
    }

}

```

## 客户端初始化配置

1. 开启了心跳事件触发器支持的功能
2. 配置了 http 编解码器
3. 配置了 handler 处理器
4. 开启了 wss 连接支持

```java
import io.netty.channel.ChannelHandler;
import io.netty.channel.ChannelInitializer;
import io.netty.channel.ChannelPipeline;
import io.netty.channel.SimpleChannelInboundHandler;
import io.netty.channel.socket.SocketChannel;
import io.netty.handler.codec.http.HttpClientCodec;
import io.netty.handler.codec.http.HttpObjectAggregator;
import io.netty.handler.ssl.SslContext;
import io.netty.handler.timeout.IdleStateHandler;
import lombok.AllArgsConstructor;

import java.util.concurrent.CountDownLatch;

/**
 * netty 客户端初始化
 */
@AllArgsConstructor
public class ClientInitializer extends ChannelInitializer<SocketChannel> {
    private CountDownLatch latch;
    private String host;
    private int port;
    private SslContext sslCtx;
    private String type;
    private SimpleChannelInboundHandler handler;
    private WebSocketClient webSocketClient;

    public ClientInitializer(CountDownLatch latch, String host, int port, SslContext sslCtx, String type, WebSocketClient webSocketClient) {
        this.latch = latch;
        this.host = host;
        this.port = port;
        this.sslCtx = sslCtx;
        this.type = type;
        this.webSocketClient = webSocketClient;
    }

    @Override
    protected void initChannel(SocketChannel sc) {
        //添加wss协议支持
        if (null != sslCtx) sc.pipeline().addLast(sslCtx.newHandler(sc.alloc(), host, port));
        //动态 handler配置支持
        switch (type) {
            case "1":
                handler = new WebSocketClientHandler(latch, webSocketClient);
                break;
            default:
                handler = new WebSocketClientHandler(latch, webSocketClient);
                break;
        }
        ChannelPipeline pipeline = sc.pipeline();
        /**
         * 添加心跳支持,超过5秒没有 ping 服务器就会触发 READER_IDLE 事件，进行ping服务器操作
         */
        pipeline.addLast(new IdleStateHandler(0, 5, 0));
        pipeline.addLast(new ChannelHandler[]{new HttpClientCodec(), new HttpObjectAggregator(1024 * 1024 * 10)});
        pipeline.addLast("websocketHandler", handler);
    }

}

```



## 客户端的 handler 处理器逻辑

大致逻辑有：完成握手、根据消息类型（BinaryWebSocketFrame、TextWebSocketFrame、FullHttpResponse）做了一个分类接收、通道断开进行重连、心跳 “起搏器” 的逻辑编写。具体的心跳机制详情参考文章末尾的附页部分

```java
import io.netty.channel.*;
import io.netty.handler.codec.http.FullHttpResponse;
import io.netty.handler.codec.http.websocketx.*;
import io.netty.handler.timeout.IdleStateEvent;
import io.netty.util.CharsetUtil;
import lombok.Data;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.util.concurrent.CountDownLatch;

@Data
public class WebSocketClientHandler extends SimpleChannelInboundHandler {
    private static final Logger logger = LoggerFactory.getLogger(WebSocketClientHandler.class);
    private WebSocketClientHandshaker handshaker;
    private ChannelPromise handshakeFuture;
    /**
     * 加入计数器的目的：由于连接是异步的，可能出现拿着还没连接成功的 channel来进行发送消息（报错），加入计数器后，只有连接成功才会放行测试类中发送消息的代码
     */
    private CountDownLatch lathc;
    private String result;
    private WebSocketClient webSocketClient;

    @Override
    public void userEventTriggered(ChannelHandlerContext ctx, Object evt){
        IdleStateEvent event = (IdleStateEvent) evt;
        switch (event.state()) {
            case READER_IDLE:
                break;
            case WRITER_IDLE:
                System.err.println("发送数据：ping");
                webSocketClient.getChannel().writeAndFlush(new TextWebSocketFrame("ping"));
                break;
            case ALL_IDLE:
                break;
            default:
                break;
        }
    }

    protected void channelRead0(ChannelHandlerContext ctx, Object msg) throws Exception {
        Channel ch = ctx.channel();
        System.err.println("通道状态：" + ctx.channel().isActive());
        System.out.println("是否握手成功：" + this.handshaker.isHandshakeComplete());
        FullHttpResponse response;
        if (!this.handshaker.isHandshakeComplete()) {
            try {
                response = (FullHttpResponse) msg;
                //完成握手
                this.handshaker.finishHandshake(ch, response);
                this.handshakeFuture.setSuccess();
                if (this.handshaker.isHandshakeComplete()) {
                    System.err.println("ws协议升级成功~");
                }
                lathc.countDown();
            } catch (WebSocketHandshakeException var7) {
                FullHttpResponse res = (FullHttpResponse) msg;
                String errorMsg = String.format("WebSocket Client failed to connect,status:%s,reason:%s", res.status(), res.content().toString(CharsetUtil.UTF_8));
                this.handshakeFuture.setFailure(new Exception(errorMsg));
            }
        } else if (msg instanceof FullHttpResponse) {
            response = (FullHttpResponse) msg;
            throw new IllegalStateException("Unexpected FullHttpResponse (getStatus=" + response.status() + ", content=" + response.content().toString(CharsetUtil.UTF_8) + ')');
        } else {
            WebSocketFrame frame = (WebSocketFrame) msg;
            if (frame instanceof BinaryWebSocketFrame) {
                BinaryWebSocketFrame webSocketFrame = (BinaryWebSocketFrame) frame;
                result = webSocketFrame.content().toString(CharsetUtil.UTF_8);
                System.err.println("BinaryWebSocketFrame数据：" + result);
            }
            if (frame instanceof TextWebSocketFrame) {
                String content = ((TextWebSocketFrame) msg).text();
                System.err.println("接收数据：" + content);
            }
        }
    }


    /**
     * 通道关闭将会触发此方法,并且进行重连1w次
     *
     * @param ctx
     * @throws Exception
     */
    @Override
    public void channelInactive(ChannelHandlerContext ctx) throws Exception {
        System.out.println("channelInactive 触发，通道关闭！" + ctx.channel().isActive());
        webSocketClient.doConnect(ctx, 10000);
    }

    public WebSocketClientHandler(CountDownLatch lathc, WebSocketClient webSocketClient) {
        this.lathc = lathc;
        this.webSocketClient = webSocketClient;
    }

    /**
     * 这个方法netty执行的时候自己会去调
     *
     * @param ctx
     */
    public void handlerAdded(ChannelHandlerContext ctx) {
        this.handshakeFuture = ctx.newPromise();
    }
}

```



## http协议连接测试

```java
  public static void main(String[] args) throws URISyntaxException, InterruptedException {
        CountDownLatch countDownLatch = new CountDownLatch(1);
        WebSocketClient webSocketClient = new WebSocketClient("http://192.168.20.7:8080/chat?uid=2", "1", countDownLatch);
        webSocketClient.connect();
        countDownLatch.await();
        webSocketClient.getChannel().writeAndFlush(new TextWebSocketFrame("hello"));
    }

```

服务器挂了客户端会进行重连，重连成功后接着发送 ping消息给服务器，证明俺是个活人
![在这里插入图片描述](https://img-blog.csdnimg.cn/323b36c25bd641299c84ce6ed939f383.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5byg5a2Q6KGM55qE5Y2a5a6i,size_20,color_FFFFFF,t_70,g_se,x_16)

## wss协议连接测试

成功连接并且接收到了数据，下面的wss测试接口是我开发中用到的接口，emmm读者可以自行寻找wss接口进行测试~~~~

![在这里插入图片描述](https://img-blog.csdnimg.cn/c5ba5790e7234a84b33a75c2f7eb173c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5byg5a2Q6KGM55qE5Y2a5a6i,size_20,color_FFFFFF,t_70,g_se,x_16)

![在这里插入图片描述](https://img-blog.csdnimg.cn/b6c6bb30301645859cfcb90280555e7e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5byg5a2Q6KGM55qE5Y2a5a6i,size_20,color_FFFFFF,t_70,g_se,x_16)

## 附页~客户端如何维护心跳

题外话提一嘴 netty 的这个心跳机制在客户端的应用：如果服务端挂了将会触发客户端的 channelInactive 方法，反之客户端挂了也会触发服务端的 channelInactive 方法，客户端在channelInactive 方法里面编写自己的重连逻辑，服务端在里面编写释放资源的逻辑即可，判断双方的服务有没有挂掉这个是很容易的，但是让你判断一些植物人一样的客户端这该怎么去判断呢（有100w个客户端连是连上了服务端，可是用户用他发个消息今天发的明天别人才收的到，通道开启了这么多，就为了给你发一条消息吗，那肯定不行啊）客户端只要存活且存在写空闲，就一直向服务端发送ping消息，如果一经发现这个客户端隔了好几个小时没有ping我的话，那我就可以认为你已经挂掉了，我就关掉这个客户端的通道。这样效率高了好多

但是~~~~~~~~~~如果你用netty正在开发心跳功能的时候，去仔细先看看人家的服务器是怎么来实现心跳的，可能人家暴露了心跳接口也说不定哦，你只需要掉一下人家的心跳接口，根据得到的响应结果就可以判断心跳是否存活了。具体业务具体分析！！！！

## 附页~服务端如何维护心跳

在服务端的 handler 中加入如下的心跳逻辑即可，emmm服务端的 handler 代码点击此处 [**如何来实现IM？～webScoket 服务端开发**](https://blog.csdn.net/qq_42875345/article/details/118269981)

```java
  		//开启心跳事件触发器支持，10秒内从通道中没有读取到数据就触发 READER_IDLE事件
        ch.pipeline().addLast(new IdleStateHandler(10000, 0, 0));

```

```java
/**
     * 心跳事件触发器
     */
    @Override
    public void userEventTriggered(ChannelHandlerContext ctx, Object evt) throws Exception {
        if (!ctx.channel().isActive()) {
            ctx.channel().close();
            MyChannelHandlerPool.channelGroup.remove(ctx.channel());
            return;
        }
        IdleStateEvent event = (IdleStateEvent) evt;
        switch (event.state()) {
            /**
             * 客户端10秒内如果没有发送 ping 消息，标明客户端已经挂了，关闭相关通道
             */
            case READER_IDLE:
                ctx.channel().writeAndFlush(new TextWebSocketFrame("你不ping我，ok，你被我关闭了"));
                ctx.channel().close();
                MyChannelHandlerPool.channelGroup.remove(ctx.channel());
                break;
            case WRITER_IDLE:
                break;
            case ALL_IDLE:
                break;
            default:
                break;
        }
    }

```

## 个人思考

可能有部分读者看完全文会去思考，你这是握手是干嘛的呢？我不握手行不行！，你不进行握手数据传输的协议都不一样，人家是一个ws/wss服务器，握手完成就代表ws/wss协议的升级完成，不握手收发数据都无效。读者也可以自行注释掉握手的代码进行测试哦



