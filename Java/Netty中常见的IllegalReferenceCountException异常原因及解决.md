# Netty中常见的IllegalReferenceCountException异常原因及解决

2018-04-28 771 words 2 mins read 6458 times read

## CONTENTS

[问题代码](https://emacsist.github.io/2018/04/28/netty中常见的illegalreferencecountexception异常原因及解决/#问题代码)[原因](https://emacsist.github.io/2018/04/28/netty中常见的illegalreferencecountexception异常原因及解决/#原因)[解决](https://emacsist.github.io/2018/04/28/netty中常见的illegalreferencecountexception异常原因及解决/#解决)

# 问题代码

```java
package hello.in;

import io.netty.buffer.ByteBuf;
import io.netty.buffer.ByteBufUtil;
import io.netty.channel.ChannelHandlerContext;
import io.netty.channel.SimpleChannelInboundHandler;
import io.netty.handler.codec.http.DefaultFullHttpResponse;
import io.netty.handler.codec.http.HttpContent;
import io.netty.handler.codec.http.HttpResponseStatus;
import io.netty.handler.codec.http.HttpVersion;


public class EchoHandler extends SimpleChannelInboundHandler<HttpContent> {
    @Override
    protected void channelRead0(final ChannelHandlerContext ctx, final HttpContent msg) {
        System.out.println("收到" + msg);
        ByteBuf echoMsg = msg.content();
        System.out.println(new String(ByteBufUtil.getBytes(echoMsg)));
        DefaultFullHttpResponse response = new DefaultFullHttpResponse(HttpVersion.HTTP_1_1, HttpResponseStatus.OK, echoMsg);
        response.headers().set("Content-Type", "text/plain");
        ctx.write(response).addListener(ChannelFutureListener.CLOSE);
    }

    @Override
    public void channelReadComplete(final ChannelHandlerContext ctx) {
        ctx.flush();
    }

    @Override
    public void exceptionCaught(final ChannelHandlerContext ctx, final Throwable cause) {
        cause.printStackTrace();
        ctx.close();
    }
}
```

上面的代码原目的是回显的, 但请求一下, 就会报:

```bash
io.netty.util.IllegalReferenceCountException: refCnt: 0, increment: 1
	at io.netty.buffer.AbstractReferenceCountedByteBuf.release0(AbstractReferenceCountedByteBuf.java:100)
	at io.netty.buffer.AbstractReferenceCountedByteBuf.release(AbstractReferenceCountedByteBuf.java:84)
	at io.netty.handler.codec.http.DefaultHttpContent.release(DefaultHttpContent.java:94)
	at io.netty.util.ReferenceCountUtil.release(ReferenceCountUtil.java:88)
    ...
```

# 原因

首先要重点强调的是: `SimpleChannelInboundHandler` 它会自动进行一次释放(即引用计数减1). 源码如下:

```java
    @Override
    public void channelRead(ChannelHandlerContext ctx, Object msg) throws Exception {
        boolean release = true;
        try {
            if (acceptInboundMessage(msg)) {
                @SuppressWarnings("unchecked")
                I imsg = (I) msg;
                channelRead0(ctx, imsg);
            } else {
                release = false;
                ctx.fireChannelRead(msg);
            }
        } finally {
            if (autoRelease && release) {
                ReferenceCountUtil.release(msg);
            }
        }
    }
```

我们继承这个类, 一般是要重写 `channelRead0()` 这个方法的, 但实际上 Netty 内部处理的是 `channelRead()` 方法, 只是它通过模板模式来进行调用而已.

然后, 我们的代码里 `DefaultFullHttpResponse response = new DefaultFullHttpResponse(HttpVersion.HTTP_1_1, HttpResponseStatus.OK, echoMsg);` 这里使用了原 `msg.content()` 的 `ByteBuf`, 然后调用 `ctx.write(response)` 后, 就会导致 `msg` 的引用计数减1了.(这时, 引用计数变成0了~)

> 可以调用 `echoMsg.refCnt();` 来获取当前引用计数值. 在 `ctx.write(...)` 前后加一行打印, 就可以发现, `ctx.write(...)` 完之后, 引用计数减少了1.

然后最后 `channelRead0()` 执行完毕返回了, `SimpleChannelInboundHandler` 的模板方法还会再一次进行释放 `release`, 这时就会触发 `IllegalReferenceCountException` 异常了.(参考 [`[翻译\]Netty中的引用计数对象`](https://emacsist.github.io/2018/04/28/翻译netty中的引用计数对象/)).

# 解决

- 如果不想创建新的数据, 则可以直接在原对象里调用 `echoMsg.retain()` 进行引用计数加1.例如:

  ```java
  @Override
  protected void channelRead0(final ChannelHandlerContext ctx, final HttpContent msg) {
      System.out.println("收到" + msg);
      ByteBuf echoMsg = msg.content();
      echoMsg.retain();
      System.out.println(new String(ByteBufUtil.getBytes(echoMsg)));
      DefaultFullHttpResponse response = new DefaultFullHttpResponse(HttpVersion.HTTP_1_1, HttpResponseStatus.OK, echoMsg);
      response.headers().set("Content-Type", "text/plain");
      ctx.write(response).addListener(ChannelFutureListener.CLOSE);
  }
  ```

即上面的 `echoMsg.retain()` 方法.

- 构造 response 对象时, 不要复用 `echoMsg` 对象, 例如:

  ```java
  DefaultFullHttpResponse response = new DefaultFullHttpResponse(HttpVersion.HTTP_1_1, HttpResponseStatus.OK, Unpooled.copiedBuffer(echoMsg));
  ```

即, 使用 `Unpooled.copiedBuffer(...)` 来复制多一份内存数据~

- 直接使用 `ChannelInboundHandlerAdapter` 自动手动处理释放, 以免像 `SimpleChannelInboundHandler` 那样导致多次释放引用计数对象~

  ```java
  package hello.in;
  
  import io.netty.buffer.ByteBuf;
  import io.netty.buffer.ByteBufUtil;
  import io.netty.buffer.Unpooled;
  import io.netty.channel.ChannelFutureListener;
  import io.netty.channel.ChannelHandlerContext;
  import io.netty.channel.ChannelInboundHandlerAdapter;
  import io.netty.handler.codec.http.DefaultFullHttpResponse;
  import io.netty.handler.codec.http.HttpContent;
  import io.netty.handler.codec.http.HttpResponseStatus;
  import io.netty.handler.codec.http.HttpVersion;
  
  
  public class EchoHandler extends ChannelInboundHandlerAdapter {
  
  @Override
  public void channelRead(final ChannelHandlerContext ctx, final Object msg) {
      if (msg instanceof HttpContent) {
          manual(ctx, (HttpContent) msg);
      }
  }
  
  protected void manual(final ChannelHandlerContext ctx, final HttpContent msg) {
      System.out.println("收到" + msg);
      ByteBuf echoMsg = msg.content();
      System.out.println(new String(ByteBufUtil.getBytes(echoMsg)));
      DefaultFullHttpResponse response = new DefaultFullHttpResponse(HttpVersion.HTTP_1_1, HttpResponseStatus.OK, echoMsg);
      response.headers().set("Content-Type", "text/plain");
      ctx.write(response).addListener(ChannelFutureListener.CLOSE);
  }
  
  @Override
  public void channelReadComplete(final ChannelHandlerContext ctx) {
      ctx.flush();
  }
  
  @Override
  public void exceptionCaught(final ChannelHandlerContext ctx, final Throwable cause) {
      cause.printStackTrace();
      ctx.close();
  }
  }
  ```

Author emacsist

LastMod 2018-04-28

License [CC BY-NC-ND 4.0](https://creativecommons.org/licenses/by-nc-nd/4.0/)