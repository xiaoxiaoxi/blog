# 基于Java和Bytemd用120行代码实现一个桌面版Markdown编辑器

[![img](https://p26-passport.byteacctimg.com/img/user-avatar/c71b636c5f57eb117fc988a6d61504d3~300x300.image)](https://juejin.cn/user/641770521628487)

[Throwable ![lv-3](https://lf3-cdn-tos.bytescm.com/obj/static/xitu_juejin_web/e108c685147dfe1fb03d4a37257fb417.svg)](https://juejin.cn/user/641770521628487)

2021年08月15日 13:10 · 阅读 634

关注

![基于Java和Bytemd用120行代码实现一个桌面版Markdown编辑器](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/2fcad6decf334ad09f4745f2b8c26d0a~tplv-k3u1fbpfcp-zoom-crop-mark:1304:1304:1304:734.awebp)

**这是我参与8月更文挑战的第2天，活动详情查看：[8月更文挑战](https://juejin.cn/post/6987962113788493831)**

## 前提

某一天点开[掘金](https://juejin.cn/)的写作界面的时候，发现了内置`Markdown`编辑器有一个`Github`的图标，点进去就是一个开源的`Markdown`编辑器项目`bytemd`（`https://github.com/bytedance/bytemd`）：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c9d48ae5eb514704a707e50031d8ebf7~tplv-k3u1fbpfcp-watermark.awebp)

这是一个`NodeJs`项目，由字节跳动提供。联想到之前业余的时候做过一些`Swing`或者`JavaFx`的`Demo`，记得`JavaFx`中有一个组件`WebView`已经支持`Html5`、`CSS3`和`ES5`，这个组件作为一个嵌入式浏览器，可以轻松地渲染一个`URL`里面的文本内容或者直接渲染一个原始的`Html`字符串。另外，由于原生的`JavaFx`的视觉效果比较丑，可以考虑引入`Swing`配合`IntelliJ IDEA`的主题提供更好的视觉效果。本文的代码基于`JDK11`开发。

## 引入依赖

很多人吐槽过`Swing`组件的视觉效果比较差，原因有几个：

- 技术小众，现在有更好的组件进行混合开发和跨平台开发
- 基于上一点原因，导致很少人会去开发`Swing`组件的`UI`，其实`Swing`的每个组件都可以重新实现`UI`的表现效果
- `compose-jb`（`JetBrains`）组件很晚才发布出来，刚好碰上`Swing`官方停止维护，后面应该更加少人会使用`Swing`做`GUI`开发

使用`Swing`并且成功了的方案最知名的就是`JetBrains`全家桶。目前来看，为了解决这个"丑"的问题，现在有比较简单的处理方案：

- 方案一：使用`compose-jb`（名字有点不好听，官方仓库为`https://github.com/JetBrains/compose-jb`）开发，这个是`JetBrains`系列的通用组件，基于`Swing`做二次封装，**不过必须使用语言`Kotlin`，有点强买强卖的嫌疑**，这列贴两个官方的图参考一下：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/3d2b6b197fa34476b1cc91a6069127f9~tplv-k3u1fbpfcp-watermark.awebp)

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/c687a6d758ba43e3adf74a61d1f429aa~tplv-k3u1fbpfcp-watermark.awebp)

- 方案二：`FormDev`（之前推出过`Swing`布局器的开发商，官网`https://www.formdev.com/flatlaf`）提供的`FlatLaf`（`Flat Look and Feel`），提供了`Light Dark IntelliJ and Darcula themes`，而且依赖少，使用起来十分简单，个人认为当前这个是`Swing UI`组件视觉效果首选

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/75882ba8cabe438b9265afdc38887987~tplv-k3u1fbpfcp-watermark.awebp)

引入`FlatLaf`和`OpenFx`的依赖：

```xml
<dependency>
    <groupId>com.formdev</groupId>
    <artifactId>flatlaf</artifactId>
    <version>1.5</version>
</dependency>
<dependency>
    <groupId>com.formdev</groupId>
    <artifactId>flatlaf-intellij-themes</artifactId>
    <version>1.5</version>
</dependency>
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-media</artifactId>
    <version>11.0.2</version>
</dependency>
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-swing</artifactId>
    <version>11.0.2</version>
</dependency>
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-web</artifactId>
    <version>11.0.2</version>
</dependency>
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-base</artifactId>
    <version>11.0.2</version>
</dependency>
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-graphics</artifactId>
    <version>11.0.2</version>
</dependency>
<dependency>
    <groupId>org.openjfx</groupId>
    <artifactId>javafx-controls</artifactId>
    <version>11.0.2</version>
</dependency>
复制代码
```

## 布局和实现

布局的实现比较简单：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4c56bd23ab4b440db5fd66793f124407~tplv-k3u1fbpfcp-watermark.awebp)

最终的`H5`文本渲染在`WebView`组件中（`JFXPanel`是`JavaFx => Swing`的适配器，`WebView`是`JavaFx`的组件，但是这里使用的外层容器都是`Swing`组件），具体的编码实现如下：

```java
public class MarkdownEditor {

    private static final int W = 1200;
    private static final int H = 1000;
    private static final String TITLE = "markdown editor";

    public static String CONTENT = "<!DOCTYPE html>\n" +
            "<html lang=\"en\">\n" +
            "<head>\n" +
            "    <meta charset=\"UTF-8\"/>\n" +
            "    <meta name=\"viewport\" content=\"width=device-width, initial-scale=1.0\"/>\n" +
            "    <title>ByteMD example</title>\n" +
            "    <link rel=\"stylesheet\" href=\"https://unpkg.com/bytemd/dist/index.min.css\"/>\n" +
            "    <link rel=\"stylesheet\" href=\"https://unpkg.com/github-markdown-css\"/>\n" +
            "    <script src=\"https://unpkg.com/bytemd\"></script>\n" +
            "    <script src=\"https://unpkg.com/@bytemd/plugin-gfm\"></script>\n" +
            "    <script src=\"https://unpkg.com/@bytemd/plugin-highlight\"></script>\n" +
            "    <style>\n" +
            "        .bytemd {\n" +
            "            height: calc(100vh - 50px);\n" +
            "        }\n" +
            "\n" +
            "        .footer {\n" +
            "            width: 100%;\n" +
            "            height: 30px;\n" +
            "            left: 0;\n" +
            "            position: absolute;\n" +
            "            bottom: 0;\n" +
            "            text-align: center;\n" +
            "        }\n" +
            "    </style>\n" +
            "</head>\n" +
            "<body>\n" +
            "<div class=\"footer\">\n" +
            "    <a href=\"https://github.com/bytedance/bytemd\">bytemd</a>\n" +
            "</div>\n" +
            "<script>\n" +
            "    const plugins = [bytemdPluginGfm(), bytemdPluginHighlight()];\n" +
            "    const editor = new bytemd.Editor({\n" +
            "        target: document.body,\n" +
            "        props: {\n" +
            "            value: '# heading\\n\\nparagraph\\n\\n> blockquote',\n" +
            "            plugins,\n" +
            "        },\n" +
            "    });\n" +
            "    editor.$on('change', (e) => {\n" +
            "        editor.$set({value: e.detail.value});\n" +
            "    });\n" +
            "</script>\n" +
            "</body>\n" +
            "</html>";

    static {
        // 初始化主题
        try {
            UIManager.setLookAndFeel(FlatIntelliJLaf.class.getName());
        } catch (Exception e) {
            throw new IllegalStateException("theme init error", e);
        }
    }

    private static JFrame buildFrame(int w, int h, LayoutManager layoutManager) {
        JFrame frame = new JFrame();
        frame.setLayout(layoutManager);
        frame.setTitle(TITLE);
        frame.setDefaultCloseOperation(WindowConstants.EXIT_ON_CLOSE);
        frame.setSize(w, h);
        Toolkit toolkit = Toolkit.getDefaultToolkit();
        int x = (int) (toolkit.getScreenSize().getWidth() - frame.getWidth()) / 2;
        int y = (int) (toolkit.getScreenSize().getHeight() - frame.getHeight()) / 2;
        frame.setLocation(x, y);
        return frame;
    }

    private static void initAndDisplay() {
        // 构建窗体
        JFrame frame = buildFrame(W, H, new BorderLayout());
        JFXPanel panel = new JFXPanel();
        Platform.runLater(() -> {
            panel.setSize(W, H);
            initWebView(panel, CONTENT);
            frame.getContentPane().add(panel);
        });
        frame.setVisible(true);
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(MarkdownEditor::initAndDisplay);
    }

    private static void initWebView(JFXPanel fxPanel, String content) {
        StackPane root = new StackPane();
        Scene scene = new Scene(root);
        WebView webView = new WebView();
        WebEngine webEngine = webView.getEngine();
        webEngine.setJavaScriptEnabled(true);
        webEngine.loadContent(content);
        root.getChildren().add(webView);
        fxPanel.setScene(scene);
    }
}
复制代码
```

`H5`文本来源于`bytemd`的原生`JS`实现例子：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/08a5bda9a69340d3a4f2e4e3485d0aa3~tplv-k3u1fbpfcp-watermark.awebp)

所有代码加上注释大概`120`多行。使用`JDK11`运行，结果如下：

![img](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/5bc094251ae6428fae79358c5386e079~tplv-k3u1fbpfcp-watermark.awebp)

目前有`2`个没有解决的问题（也有可能是）：

- `JS`的动作触发有轻微延迟
- `WebView`组件初始化比较慢

## 小结

`Oracle JDK`官方已经宣布不再维护`Swing`项目，按照一般的尿性后面有可能从`JDK`中移除，也许是因为它体现不了自身的价值（低情商：不赚钱）。`Swing`的开发中布局是比较反人类的，一般可能一个`Swing`项目布局会耗费`90%`以上的时间，原生组件的`UI`设计看上去比较"丑"，没有丰富的扩展组件和活跃的社区，加上现在有其他更好的跨平台开发方案如`Qt`、`React Native`和`Flutter`等等，`Swing`被遗忘是一个既定的结局。往后除了一枝独秀的`JetBrains`，`Swing`的结局就是成为少数人业务的爱好，成为`JDK GUI`编程爱好者的收藏品。

`Demo`源码：

- [local-markdown-editor(`https://gitee.com/throwableDoge/local-markdown-editor`)](https://link.juejin.cn/?target=https%3A%2F%2Fgitee.com%2FthrowableDoge%2Flocal-markdown-editor)

（本文完 e-a-20210815 c-1-d）