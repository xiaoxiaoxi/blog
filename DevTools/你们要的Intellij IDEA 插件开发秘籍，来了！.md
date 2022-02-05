# 你们要的Intellij IDEA 插件开发秘籍，来了！

2018-09-28阅读 44.5K0

## 来这里找志同道合的小伙伴！

**作者简介**

王昭霞，软件开发工程师，先后从事脚本工具编写、工具开发、Android基础模块开发等工作。

大家在使用Android Studio开发的时候都会使用一些插件，来方便我们的开发工作，提升工作效率。在进行手机京东Android客户端瘦身工作时，我们将压缩图片的相关功能封装成了 IDEA 插件：ImgOptimi 图片优化工具（参考链接http://sdk.av.jd.com/share/ImgOptimi/img-optimi.html）。这里总结一下 Intellij IDEA 插件开发的知识，供大家参考。

本篇文章包含以下内容：

- 开发环境搭建
- Component 介绍
- Extension Point And Extension 介绍
- Service 介绍
- 持久化状态
- 添加插件依赖
- GUI 工具介绍

## **>>>>  IntelliJ IDEA 与 IntelliJ Platform**

IntelliJ IDEA 简称 IDEA，是 Jetbrains 公司旗下的一款 JAVA 开发工具，支持 Java、Scala、Groovy 等语言的开发，同时具备支持目前主流的技术和框架，擅长于企业应用、移动应用和 Web 应用的开发，提供了丰富的功能，智能代码助手、代码自动提示、重构、J2EE支持、各类版本工具(git、svn等)、JUnit、CVS整合、代码分析、 创新的GUI设计等。

IntelliJ Platform 是一个构建 IDE 的开源平台，基于它构建的 IDE 有 IntelliJ IDEA、WebStorm、DataGrip、以及 Android Studio 等等。IDEA 插件也是基于 IntelliJ Platform 开发的。

## **>>>>  开发环境搭建**

本章节介绍 IDEA 插件开发环境的搭建与配置

## **>>>>  一、开发工具**

开发工具使用 Intellij IDEA，下载地址：https://www.jetbrains.com/idea/

IDEA 分为两个版本：

- 社区版（Community）：完全免费，代码开源，但是缺少一些旗舰版中的高级特性
- 旗舰版（Ultimate）：30天免费，支持全部功能，代码不开源

开发IDEA的插件推荐使用社区版，因为社区版是开源的，在开发插件的时候，可以调试源代码。

## **>>>>  二、启用 Plugin DevKit**

Plugin DevKit 是 IntelliJ 的一个插件，它使用 IntelliJ IDEA 自己的构建系统来为开发 IDEA 插件提供支持。开发 IDEA 插件之前需要安装并启用 **Plugin DevKit** 。

打开 IDEA，导航到 **Settings | Plugins**，若插件列表中没有 **Plugin DevKit**，点击 **Install JetBrains plugin**，搜索并安装。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/8g89atskcs.jpeg?imageView2/2/w/1620)

## **>>>>  三、配置 IntelliJ Platform Plugin SDK**

IntelliJ Platform Plugin SDK 就是开发 IntelliJ 平台插件的SDK, 是基于 JDK 之上运行的，类似于开发 Android 应用需要 Android SDK。

1. 导航到 **File | Project Structure**，选择对话框左侧栏 **Platform Settings** 下的 **SDKs**
2. 点击 **+** 按钮，先选择 **JDK**，指定 JDK 的路径；再创建 **IntelliJ Platform Plugin SDK**，指定 home path 为 IDEA 的安装路径，如图

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/m1k1w2240f.jpeg?imageView2/2/w/1620)

1. 创建好 IntelliJ Platform Plugin SDK 后，选择左侧栏 **Project Settings** 下的 **Projects**，在 **Project SDK** 下选择刚创建的 IntelliJ Platform Plugin SDK。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/3sh3l26sww.png?imageView2/2/w/1620)

## **>>>>  四、设置源码路径（可选）**

1. 查看 build 号：打开 IDEA，**Help | About**，查看版本号及 build 号
2. IDEA Community 源码（https://github.com/JetBrains/intellij-community/）：**切换到与 build 号相同的分支**，点击 **Clone or download** 按钮，选择 **Download ZIP**

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/gwvnlfzuu0.jpeg?imageView2/2/w/1620)

## **>>>>  五、Sandbox**

IntelliJ IDEA 插件以 Debug/Run 模式运行时是在 SandBox 中进行的，不会影响当前的 IntelliJ IDEA；但是同一台机器同时开发多个插件时默认使用的同一个 sandbox，即在创建 IntelliJ Platform SDK 时默认指定的 Sandbox Home

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/6exhodt8u1.png?imageView2/2/w/1620)

如果需要每个插件的开发环境是相互独立的，可以创建多个 IntelliJ Platform SDK，为 Sandbox Home 指定不同的目录 。

## **>>>>  开发一个简单插件**

本篇介绍插件的创建、配置、运行、打包流程，以及 action

## **>>>>  一、创建一个插件工程**

选择 **File | New | Project**，左侧栏中选择 **IntelliJ Platform Plugin** 工程类型

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/ku60d58uh0.png?imageView2/2/w/1620)

点击 **Next**，设置工程名称及位置，点击 **Finish** 完成创建。可以到 File | Project Structure 来自定义工程设置。

## **>>>>  二、插件工程结构**

插件工程内容：

```javascript
PluginDemo/
    resources/
      META-INF/
        plugin.xml
    src/
      com/foo/...
      ...
      ...
```

- **src** 实现插件功能的classes
- **resources/META-INF/plugin.xml** 插件的配置文件，指定插件名称、描述、版本号、支持的 IntelliJ IDEA 版本、插件的 components 和 actions 以及软件商等信息。

## **>>>>  三、plugin.xml**

下面示例描述了可在 plugin.xml 文件配置的主要元素：

```javascript
<idea-plugin>

  <!-- 插件名称，别人在官方插件库搜索你的插件时使用的名称 -->
  <name>MyPlugin</name>

  <!-- 插件唯一id，不能和其他插件项目重复，所以推荐使用com.xxx.xxx的格式
       插件不同版本之间不能更改，若没有指定，则与插件名称相同 -->
  <id>com.example.plugin.myplugin</id>

  <!-- 插件的描述 -->
  <description>my plugin description</description>

  <!-- 插件版本变更信息，支持HTML标签；
       将展示在 settings | Plugins 对话框和插件仓库的Web页面 -->
  <change-notes>Initial release of the plugin.</change-notes>

  <!-- 插件版本 -->
  <version>1.0</version>

  <!-- 供应商主页和email-->
  <vendor url="http://www.jetbrains.com" email="support@jetbrains.com" />

  <!-- 插件所依赖的其他插件的id -->
  <depends>MyFirstPlugin</depends>

  <!-- 插件兼容IDEA的最大和最小 build 号，两个属性可以任选一个或者同时使用
       官网详细介绍：http://www.jetbrains.org/intellij/sdk/docs/basics/getting_started/build_number_ranges.html-->
  <idea-version since-build="3000" until-build="3999"/>

  <!-- application components -->
  <application-components>
    <component>
      <!-- 组件接口 -->
      <interface-class>com.foo.Component1Interface</interface-class>
      <!-- 组件的实现类 -->
      <implementation-class>com.foo.impl.Component1Impl</implementation-class>
    </component>
  </application-components>

  <!-- project components -->
  <project-components>
    <component>
      <!-- 接口和实现类相同 -->
      <interface-class>com.foo.Component2</interface-class>
    </component>
  </project-components>

  <!-- module components -->
  <module-components>
    <component>
      <interface-class>com.foo.Component3</interface-class>
    </component>
  </module-components>

  <!-- Actions -->
  <actions>
    ...
  </actions>

  <!-- 插件定义的扩展点，以供其他插件扩展该插件 -->
  <extensionPoints>
    ...
  </extensionPoints>

  <!-- 声明该插件对IDEA core或其他插件的扩展 -->
  <extensions xmlns="com.intellij">
    ...
  </extensions>
</idea-plugin>
```

## **>>>>  四、创建 Action**

一个 Action 表示 IDEA 菜单里的一个 menu item 或工具栏上的一个按钮，通过继承 `AnAction` class 实现，当选择一个 menu item 或点击工具栏上的按钮时，就会调用 AnAction 类的 `actionPerformed` 方法。

实现自定义 Action 分两步：

- 定义一个或多个 action
- 注册 action，将 item 添加到菜单或工具栏上

#### 

#### 

#### **1、定义 Action**

定义一个 Java class，继承 `AnAction` 类，并重写 `actionPerformed` 方法， 如

```javascript
public class TextBoxes extends AnAction {

    public void actionPerformed(AnActionEvent event) {
        Project project = event.getData(PlatformDataKeys.PROJECT);
        Messages.showInputDialog(
          project,
          "What is your name?",
          "Input your name",
          Messages.getQuestionIcon());
    }
}
```

#### 

#### **2、注册 Action**

在 plugin.xml 文件的 `<actions>` 元素内注册

```javascript
<actions>
  <group id="MyPlugin.SampleMenu" text="Sample Menu" description="Sample menu">
    <add-to-group group-id="MainMenu" anchor="last"  />
       <action id="Myplugin.Textboxes" class="Mypackage.TextBoxes" text="Text Boxes" description="A test menu item" />
  </group>
</actions>
```

- `<action>` 元素会定义一个 action，指定 action 的 id、实现类、显示文本、描述
- `<group>` 元素会定义一个 action group（多个action），设置 action group 的 id、文本、描述
- `<add-to-group>` 元素指定其外部 action 或 action group 被添加到的位置

上面示例会定义一个被添加到 IDEA 主菜单的最后面的 “SampleMenu” 的菜单，点击该菜单将弹出一个 “Text Boxes” item，如图

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/ppbcfyey82.png?imageView2/2/w/1620)

点击该 “Text Boxes” item，弹出一个提示输入名字的对话框

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/1fu35lj5y5.png?imageView2/2/w/1620)

更多 action 信息请移步 *IntelliJ Platform Action System*（http://www.jetbrains.org/intellij/sdk/docs/basics/action_system.html）

#### **3、快速创建 Action**

IntelliJ Platform 提供了 **New Action** 向导，它会帮助我们创建 action class 并配置 plugin.xml 文件：

在目标 package 上右键，选择 **New | Plugin DevKit | Action**：

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/u7s0zatvri.jpeg?imageView2/2/w/1620)

在弹出的对话框中填充下列字段，然后点击 OK：

- **Action ID**: action 唯一 id，推荐 format: `PluginName.ID`
- **Class Name**: 要被创建的 action class 名称
- **Name**: menu item 的文本
- **Description**: action 描述，toolbar 上按钮的提示文本，可选
- **Add to Group**：选择新 action 要被添加到的 action group（**Groups, Actions**）以及相对其他 actions 的位置（**Anchor**）
- **Keyboard Shortcuts**：指定 action 的第一和第二快捷键

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/7f2kaxe664.png?imageView2/2/w/1620)

注意：该向导只能向主菜单中已存在的 action group 或工具栏上添加 action，若要创建新的 action group，请参考前面的内容。

## **>>>>  五、运行调试插件**

运行/调试插件可直接在 IntelliJ IDEA 进行，选择 **Run | Edit Configurations...**，若左侧栏没有 Plugin 类型的 Configuration, 点击右上角 **+** 按钮，选择 **Plugin** 类型, 如图

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/mzcmalgtpv.jpeg?imageView2/2/w/1620)

**Use classpath of module** 选择要调试的 module，其余配置一般默认即可；切换到 Logs 选项卡，如果勾选了 idea.log，运行插件时 idea.log 文件的内容将输出到 idea.log console。

运行插件点击工具栏上

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/7n83rn0fq.png?imageView2/2/w/1620)

按钮即可，IntelliJ IDEA 会另启一个装有该插件的 IDEA 窗口

## **>>>>  六、打包安装插件**

#### **1、打包插件**

选择 **Build | Prepare Plugin Module ‘module name’ for Deployment** 来打包插件：

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/xsxjy8rsg7.png?imageView2/2/w/1620)

插件包位置：一般在工程根目录下

如果插件没有依赖任何 library，插件会被打包成一个 `.jar`，否则会被打包成一个 `.zip`，zip 中包含了所有的插件依赖

jar类型的插件包：

```javascript
PluginDemo.jar/
  com/foo/...
  ...
  ...
  META-INF/
    plugin.xml
```

zip类型的插件包：

```javascript
PluginDemo.zip/
  lib/
    libfoo.jar
    libbar.jar
    PluginDemo.jar/
      com/foo/...
      ...
      ...
      META-INF/
        plugin.xml
```

#### **2、安装插件**

- 导航到 **File | Settings | Plugins** 页面，点击 **Install plugin from disk...**

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/r9wbxnekoh.jpeg?imageView2/2/w/1620)

- 选择插件包的位置，点击 OK
- 在插件列表中，勾选插件名字后面的 check-box 来启用插件，点击 OK
- 重启 IDEA

**Install JetBrains plugin...** 从 *JetBrains 仓库*（https://plugins.jetbrains.com/）中安装插件

**Browse repositories...** 添加并管理自己的仓库

## **>>>>  Components**

IntelliJ IDEA 的组件模型是基于 *PicoContainer*（https://www.cnblogs.com/yaoxiaohui/archive/2009/03/08/1406228.html） 的，组件都包含在这些容器中，但容器有三种级别：application container，project container 以及 module container。application container 可以包含多个 project container，而 project container 可以包含多个 module container。

## **>>>>  一、Components 类型**

Components 是插件开发的基础，Components 有三种类型：

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/2nmtbfazct.jpeg?imageView2/2/w/1620)

## **>>>>  二、注册 Components**

components 需要配置在 plugin.xml 中，并指定 interface 和 implementation，interface 类用于从其他组件中检索组件，implementation 类用于实例化组件。示例：

```javascript
//创建一个 application level component
public interface Component1 extends ApplicationComponent {
}

public class Component1Impl implements Component1 {

    @Override
    public String getComponentName() {
        return "PluginDemo.Component1";
    }
}
```

plugin.xml

```javascript
<application-components>
    <component>
      <interface-class>com.example.test.Component1</interface-class>
      <implementation-class>com.example.test.Component1Impl</implementation-class>
    </component>
  </application-components>
```

注意：

1. 一个 interface-class 不能有多个 implementation-class，如下图：

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/2vird2sem2.jpeg?imageView2/2/w/1620)

1. 若组件没有创建 interface 类，而是直接实现了 ApplicationComponent 等接口，interface 和 implementation 可以指定为同一个类。
2. 每一个组件都应该有一个唯一的名字，通过 `getComponentName()` 返回，推荐使用 `<plugin_name>.<component_name>` 格式。

## **>>>>  三、Component 周期方法**

ApplicationComponent 的生命周期方法：

```javascript
//构造方法
public constructor(){
}
//初始化
public void initComponent() {
}

public void disposeComponent() {
}
```

ProjectComponent 的生命周期方法：

```javascript
//构造方法
public constructor(){
}
//通知一个project已经完成加载
public void projectOpened() {
}

public void projectClosed() {
}
//执行初始化操作以及与其他 components 的通信
public void initComponent() {
}
//释放系统资源或执行其他清理
public void disposeComponent() {
}
```

ModuleComponent 的生命周期方法：

ModuleComponent 的生命周期方法中比 ProjectComponent 多一个 `moduleAdded()`，用于通知 module 已经被添加到 project 中。

## **>>>>  四、Component 加载**

Application 级别的 components 在 IDEA 启动时加载，Project 和 Module 级别的 components 在项目启动时共同加载。

一个组件加载过程：

1. 创建：调用构造方法
2. 初始化：调用 `initComponent()` 方法
3. 如果是 Project 组件，会调用 `projectOpened()` 方法； 如果是 Module 组件，会依次调用 `moduleAdded()` 和 `projectOpened()` 方法

如果 component 在加载时需要用到其他 component，我们只需在该 component 的构造方法的参数列表声明即可，在这种情况下，IntelliJ IDEA 会按正确的顺序实例化所依赖的 component。

示例：

```javascript
public class MyComponent implements ApplicationComponent {
    private final MyOtherComponent otherComponent;

    public MyComponent(MyOtherComponent otherComponent) {
       this.otherComponent = otherComponent;
    }
    ...
}
```

## **>>>>  五、Component 卸载**

一个组件卸载过程：

1. 如果是 Project 或 Module 组件，调用 `projectClosed()`
2. 接下来 `disposeComponent()` 将被调用

## **>>>>  六、Component 容器**

前面我们提到有三种不同的容器，application container 实现 Application 接口; project container 实现 Project 接口;

module container 实现 Module 接口。每一个容器都有自己的方法去获取容器内的 component。

获取 application 容器及其内部的组件：

```javascript
//获取application容器
Application application = ApplicationManager.getApplication()；
//获取application容器中的组件
MyComponent myComponent = application.getComponent(MyComponent.class);
```

获取 project / module 容器及其内部的组件：

在 component 构造方法的参数列表中声明：

```javascript
public class MyComponent implements ProjectComponent {
Project project;
public MyComponent(Project project){
this.project = project;
}

public void initComponent() {
OtherComponent otherComponent = project.getComponent(OtherComponent.class);
}
}
```

在这个例子中，组件在构造方法中获取了容器对象，将其保存，然后在 component 其他地方进行引用。但是需要注意一点：

> Be careful when passing this reference to other components (especially >application-level ones). If an application- level component does not release the reference, but saves it inside itself, >all the resources used by a project or module will not be unloaded from the memory on the project closing.

或者从action的事件处理的context的获取：

```javascript
public class TextBoxes extends AnAction {
    @Override
    public void actionPerformed(AnActionEvent anActionEvent) {
        DataContext dataContext = e.getDataContext();
        Project project = (Project)dataContext.getData(DataConstants.PROJECT);
        Module module =(Module)dataContext.getData(DataConstants.MODULE);
    }
}
```

## **>>>>  Extensions and Extension Points**

如果插件需要扩展 IDEA Platform 或 其他插件的功能，或为其他插件提供可以扩展自己的接口，那么就要用到 extensions 和 extension points，用于与 IDEA 和其他插件交互。

## **>>>>  一、Extension points**

extension point 用于数据信息扩展，使其他插件可以扩展本插件的功能，可通过plugin.xml 的 `<extensionPoints>` 元素声明，如下示例：

```javascript
<extensionPoints>
    <!--使用beanClass声明-->
    <extensionPoint name="MyExtensionPoint1" beanClass="MyPackage.MyBeanClass" area="IDEA_APPLICATION">
        <with attribute="implementationClass" implements="MyPackage.MyAbstractClass"/>
    </extensionPoint>
    <!--使用interface声明-->
    <extensionPoint name="MyExtensionPoint2" interface="MyPlugin.MyInterface" area="IDEA_PROJECT" />
</extensionPoints>
```

- **name** 指定 extension point 的名字，当其他插件扩展该extensionPoint时，需要指定该name
- **area** 有三种值，IDEAAPPLICATION，IDEAPROJECT，IDEA_MODULE，指定extension point的级别
- **interface** 指定需要扩展此 extension point 的插件必须要实现的接口
- **beanClass** 指定一个类，该类有一个或多个被 *`@Attribut`*`e` （https://upsource.jetbrains.com/idea-ce/file/idea-ce-d00d8b4ae3ed33097972b8a4286b336bf4ffcfab/xml/dom-openapi/src/com/intellij/util/xml/Attribute.java）注解的属性
- 声明 extension point 有两种方式，指定 beanClass 或 interface
- 如果某个属性需要是某个类的子类，或某个接口的实现类，需要通过 `<with>` 指明类名或接口名。

示例上述代码中的 MyExtensionPoint1 的 beanClass：

```javascript
public class MyBeanClass extends AbstractExtensionPointBean {
  @Attribute("key")
  public String key;

  @Attribute("implementationClass")
  public String implementationClass;

  ...
}
```

## **>>>>  二、Extension**

如果插件需要扩展 IntelliJ Platform 或其他插件的功能，需要声明一个或多个 extension。

1. 设置 `<extensions>` 的 `defaultExtensionNs` 属性 若是扩展 IntelliJ Platform，设为 `com.intellij` 若是扩展其他插件，则设为 `pluginId`
2. 指定要扩展哪个 extension point内部的子标签的名字必须与 extension point 的 name 属性相同
3. 如果 extension point 

- 是通过 `interface` 声明的，那么使用 `implementation` 属性指明 interface 的实现类
- 是通过 `beanClass` 声明的，那么就要为 beanClass 中被 `@Attribute` 注解的属性指定属性值

示例：

```javascript
<!-- 扩展 interface 声明的 extensionPoint -->
  <extensions defaultExtensionNs="com.intellij">
    <appStarter implementation="MyPackage.MyExtension1" />
    <applicationConfigurable implementation="MyPackage.MyExtension2" />
  </extensions>

  <!-- 扩展 beanClass 声明的 extensionPoint -->
  <extensions defaultExtensionNs="pluginId">
     <MyExtensionPoint1 key="keyValue" implementationClass="MyPackage.MyClassImpl"></MyExtensionPoint1>
  </extensions>
```

插件的 service 的实现就是扩展 IDEA Platform 的 `applicationService` 或 `projectService` 两个 extension points

## **>>>>  三、获取 extension points**

IntelliJ Platform 的 extension points：

- *LangExtensionPoints.xml*（https://upsource.jetbrains.com/idea-ce/file/idea-ce-d00d8b4ae3ed33097972b8a4286b336bf4ffcfab/platform/platform-resources/src/META-INF/LangExtensionPoints.xml）
- *PlatformExtensionPoints.xml*（https://upsource.jetbrains.com/idea-ce/file/idea-ce-d00d8b4ae3ed33097972b8a4286b336bf4ffcfab/platform/platform-resources/src/META-INF/PlatformExtensionPoints.xml）
- *VcsExtensionPoints.xml*（https://upsource.jetbrains.com/idea-ce/file/idea-ce-d00d8b4ae3ed33097972b8a4286b336bf4ffcfab/platform/platform-resources/src/META-INF/VcsExtensionPoints.xml）

其他插件的 extension points：可以从被扩展插件的 plugin.xml 文件中获取

## **>>>>  Service**

Service 也是一种按需加载的 component，在调用 *`ServiceManager.getService(Class)`*（https://upsource.jetbrains.com/idea-ce/file/idea-ce-d00d8b4ae3ed33097972b8a4286b336bf4ffcfab/platform/core-api/src/com/intellij/openapi/components/ServiceManager.java）时才会加载，且程序中只有一个实例。

Serivce 在 IntelliJ IDEA 中是以 extension point 形式提供的，实现自己的 service 需要扩展相应 extension point。

- applicationService: application level service
- projectService: project level service
- moduleService: module level service

声明 service 时必须包含 `serviceImplementation` 属性用于实例化 service， `serviceInterface` 属性是可选的，可用于获取 service 实例。

## **>>>>  一、创建 Service**

在需要放置 service 的 package 上右键， **New | Plugin DevKit | xxxxService**，如图

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/ef84117th.jpeg?imageView2/2/w/1620)

选择相应 service，弹出如下对话框，填写 interface 类和 implementation 类，若不勾选 **Separate interface from implementation**，只需填写 implementation 类。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/j4fjz40r66.png?imageView2/2/w/1620)

IntelliJ IDEA 会自动创建相应类并配置 plugin.xml 文件。

示例：

plugin.xml：

```javascript
<extensions defaultExtensionNs="com.intellij">
    <!-- project level service -->
    <projectService serviceInterface="com.example.test.service.MyProjectService"
                    serviceImplementation="com.example.test.service.impl.MyProjectServiceImpl"/>
  </extensions>
```

生成的 service 类：

```javascript
package com.example.test.service;

import com.intellij.openapi.components.ServiceManager;
import com.intellij.openapi.project.Project;
import org.jetbrains.annotations.NotNull;

public interface MyProjectService {
    //获取 service 实例
    static MyProjectService getInstance(@NotNull Project project) {
        return ServiceManager.getService(project, MyProjectService.class);
    }
}
package com.example.test.service.impl;

import com.example.test.service.MyProjectService;
import com.intellij.openapi.project.Project;
public class MyProjectServiceImpl implements MyProjectService {
    public MyProjectServiceImpl(Project project) {
    }
}
```

## **>>>>  二、获取 Service**

```javascript
MyApplicationService applicationService = ServiceManager.getService(MyApplicationService.class);

//获取 project 级别的 service，需要提供 project 对象
MyProjectService projectService = ServiceManager.getService(project, MyProjectService.class);

//获取 module 级别的 service，需要提供 module 对象
MyModuleService moduleService = ModuleServiceManager.getService(module, MyModuleService.class);
```

## **>>>>  持久化状态**

我们在使用 IDE 开始开发工作之前，总是要先在 settings 页面进行一些设置，且每次重新打开 IDE 后这些设置仍然保留着，那么这些设置是如何保存下来的呢？

IntelliJ Platform 提供了一些 API，可以使 components 或 services 在每次打开 IDE 时仍然使用之前的数据，即持久化其状态。

## **>>>>  一、PropertiesComponent**

对于一些简单少量的值，我们可以使用 `PropertiesComponent`，它可以保存 application 级别和 project 级别的值。

下面方法用于获取 PropertiesComponent 对象：

```javascript
//获取 application 级别的 PropertiesComponent
PropertiesComponent.getInstance()
//获取 project 级别的 PropertiesComponent，指定相应的 project
PropertiesComponent.getInstance(Project)

propertiesComponent.setValue(name, value)
propertiesComponent.getValue(name)
```

`PropertiesComponent` 保存的是键值对，由于所有插件使用的是同一个 namespace，强烈建议使用前缀来命名 name，比如使用 plugin id。

## **>>>>  二、PersistentStateComponent**

*PersistentStateComponent*（https://upsource.jetbrains.com/idea-ce/file/idea-ce-d00d8b4ae3ed33097972b8a4286b336bf4ffcfab/platform/projectModel-api/src/com/intellij/openapi/components/PersistentStateComponent.java） 用于持久化比较复杂的 components 或 services，可以指定需要持久化的值、值的格式以及存储位置。

要使用 `PersistentStateComponent` 持久化状态：

- 需要提供一个 `PersistentStateComponent<T>` 接口的实现类（component 或 service），指定类型参数，重写 getState() 和 loadState() 方法
- 类型参数就是要被持久化的类，它可以是一个 bean class，也可以是 `PersistentStateComponent`实现类本身。
- 在 `PersistentStateComponent<T>` 的实现类上，通过 `@com.intellij.openapi.components.State` 注解指定存储的位置

下面通过两个例子进行说明：

```javascript
class MyService implements PersistentStateComponent<MyService.State> {
  //这里 state 是一个 bean class
  static class State {
    public String value;
    ...
  }

  //用于保存当前的状态
  State myState;

  // 从当前对象里获取状态
  public State getState() {
    return myState;
  }
  // 从外部加载状态，设置给当前对象的相应字段
  public void loadState(State state) {
    myState = state;
  }
}
// 这里的 state 就是实现类本身
class MyService implements PersistentStateComponent<MyService> {
  public String stateValue;
  ...

  public MyService getState() {
    return this;
  }

  public void loadState(MyService state) {
    XmlSerializerUtil.copyBean(state, this);
  }
}
```

#### **1、实现 State 类**

**a、字段要求**

state 类中可能有多个字段，但不是所有字段都可以被持久化，可以被持久化的字段：

- public 字段
- bean 属性：提供 getter 和 setter 方法
- 被*注解*（https://upsource.jetbrains.com/idea-ce/file/idea-ce-d00d8b4ae3ed33097972b8a4286b336bf4ffcfab/platform/util/src/com/intellij/util/xmlb/annotations）的私有字段：使用 @Tag, @Attribute, @Property, @MapAnnotation, @AbstractCollection 等注解来自定义存储格式，一般在实现向后兼容时才考虑使用这些注解

这些字段也有类型要求：

- 数字（包括基础类型，如int，和封装类型，如Integer）
- 布尔值
- 字符串
- 集合
- map
- 枚举

如果不希望某个字段被持久化，可以使用 `@com.intellij.util.xmlb.annotations.Transient` 注解。

**b、构造器要求**

state 类必须有一个默认构造器，这个构造器返回的 state 对象被认为是默认状态，只有当当前状态与默认状态不同时，状态才会被持久化。

#### **2、定义存储位置**

我们可以使用 `@State` 注解来定义存储位置

```javascript
@State(name = "PersistentDemo", storages = {@Storage(value = "PluginDemo.xml")})
public class PersistentDemo implements PersistentStateComponent<PersistentDemo> {
  ...
}
```

**name：** 定义 xml 文件根标签的名称

**storages：** 一个或多个 `@Storage`，定义存储的位置

- 若是 application 级别的组件 运行调试时 xml 文件的位置： `~/IdeaICxxxx/system/plugins-sandbox/config/options` 正式环境时 xml 文件的位置： `~/IdeaICxxxx/config/options`
- 若是 project 级别的组件，默认为项目的 `.idea/misc.xml`，若指定为 `StoragePathMacros.WORKSPACE_FILE`，则会被保存在 `.idea/worksapce.xml`

#### **3、生命周期**

- **loadState()** 当组件被创建或 xml 文件被外部改变（比如被版本控制系统更新）时被调用
- **getState()** 当 settings 被保存（比如settings窗口失去焦点，关闭IDE）时，该方法会被调用并保存状态值。如果 `getState()` 返回的状态与默认状态相同，那么什么都不会被保存。
- **noStateLoaded()** 该方法不是必须实现的，当初始化组件，但是没有状态被持久化时会被调用

#### **4、组件声明**

持久化组件可以声明为 component，也可以声明为 service

声明为 service，plugin.xml 文件如下配置：

```javascript
<extensions defaultExtensionNs="com.intellij">
    <applicationService serviceImplementation="com.example.test.persisting.PersistentDemo"/>
    <projectService serviceImplementation="com.example.test.persisting.PersistentDemo2"/>
  </extensions>
```

代码中获取状态与获取 service 的方式一样：

```javascript
PersistentDemo persistDemo = ServiceManager.getService(PersistentDemo.class);
PersistentDemo2 persistDemo2 = ServiceManager.getService(project，PersistentDemo.class);
```

声明为 component，plugin.xml 文件如下配置：

```javascript
<application-components>
  <!--将持久化组件声明为component-->
  <component>
    <implementation-class>com.example.persistentdemo.PersistentComponent</implementation-class>
  </component>
</application-components>
```

获取状态与获取 component 的方式一样：

```javascript
public static PersistentComponent getInstance() {
    return ApplicationManager.getApplication().getComponent(PersistentComponent.class);
}
public static PersistentComponent getInstance(Project project) {
    return project.getComponent(PersistentComponent.class);
}
```

## **>>>>  插件依赖**

开发插件时可能会用到其他插件，可能是 IDEA 绑定的，也可能是第三方的插件。

配置插件依赖需要将插件包添加到 SDK 的 classpath 中，并在 plugin.xml 配置。

1. 确定插件包的位置 如果插件是 IDEA 捆绑的插件，那么插件包在 IDEA 安装目录的 `plugins/<pluginname>` 或 `plugins/<pluginname>/lib` 下。 如果插件是第三方或自己的，那么需要先运行一次 sandbox（其实我们在运行调试插件的时候就是在运行sandbox）并从本地或插件仓库安装依赖插件。 安装好后，插件包会放在 sandbox 目录下的 `config/plugins/<pluginname>` 或 `config/plugins/<pluginname>/lib`， 查看 sandbox 目录：打开 IntelliJ Platform SDK 配置页面，其中 **Sandbox Home** 就是其目录。
2. 将插件包添加到 SDK 的 classpath 中 导航到 **File | Project Structure | SDKs**，选择插件使用的 **IntelliJ Platform SDK**，点击右侧 **+** 号，在弹出的文件选择框中选择要依赖的插件包，点击 **OK**。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/oiavvp8jc8.jpeg?imageView2/2/w/1620)

1. 配置 plugin.xml 在 plugin.xml 的 `<depends>` 部分添加所依赖插件的id。

```javascript
<depends>org.jetbrains.kotlin</depends>
```

 plugin id 可以从插件包的 plugin.xml 文件查看。

## **>>>>  GUI 介绍**

GUI 是 IntelliJ IDEA 提供的一个自动生成 java 布局代码的工具，它使用 JDK 中的 Swing 控件来实现 UI 界面。

使用步骤：

1. 配置 GUI 首先打开 **Settings** 对话框，选择 **Editor | GUI Designer**，如图，在 **Generate GUI into:** 有两个选项，生成 class 文件或 java 代码，我们选择生成 java 代码，因为建好布局后可能需要修改代码。其他默认即可。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/gdt25cqvkw.png?imageView2/2/w/1620)

1. 创建 form 文件 form 文件用于记录界面布局。在相应的 package 上右键，选择 **New | GUI Form**，如图，输入 form 文件名，一般与 java 文件名相同，点击 OK 创建 form 与 java 文件。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/40izwu14t0.png?imageView2/2/w/1620)

1. 编辑界面 打开 form 文件，如图，通过拖拽控件来搭建布局。每个form文件布局的 root 控件都是一个 `JPanel`,可将该 root 对象传给需要该布局的类。 注意：左下角的属性面板，只有当填写了 **field name** 属性时该控件的对象才会被当成成员变量，否则为局部变量。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/7p8yb580g2.jpeg?imageView2/2/w/1620)

1. 生成 java 代码 搭建好布局后，点击

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/63xq2f2as9.png?imageView2/2/w/1620)

编译按钮，即可生成 java 的源码文件。 GUI 生成的方法名前后都有三个 `$` 标识，当再次修改布局时，GUI 只会修改 `$` 标识的方法。

![img](https://ask.qcloudimg.com/http-save/yehe-1623505/gijd1hymu8.jpeg?imageView2/2/w/1620)

本文分享自微信公众号 - 京东技术（jingdongjishu）

原文出处及转载信息见文内详细说明，如有侵权，请联系 yunjia_community@tencent.com 删除。

原始发表时间：2018-09-07

本文参与[腾讯云自媒体分享计划](https://cloud.tencent.com/developer/support-plan)，欢迎正在阅读的你也加入，一起分享。

[其他](https://cloud.tencent.com/developer/tag/125?entry=article)

[举报](javascript:;)

点赞 26分享

### 我来说两句

10 条评论

[登录](javascript:;) 后参与评论

[用户9392003](https://cloud.tencent.com/developer/user/9392003)

19小时前

厉害

[回复](javascript:;)

[rookie0peng](https://cloud.tencent.com/developer/user/7989760)

2021-01-14

大佬太强了

[回复](javascript:;)

[用户6210411](https://cloud.tencent.com/developer/user/6210411)

2020-07-10

非常感谢！很有帮助！

[回复](javascript:;)

[用户6517124](https://cloud.tencent.com/developer/user/6517124)

2019-10-21

请教大神一个问题，能否使用javaFx 开发idea 插件，我使用javaFx但启动报错

[回复](javascript:;)

[用户5976244](https://cloud.tencent.com/developer/user/5976244)

2019-08-06

牛牛牛，收藏一波。

[回复](javascript:;)

[用户4626684](https://cloud.tencent.com/developer/user/4626684)

2019-04-19

请问一下博主, 如果我想依赖我已经写好的jar包, 除了新建lib目录还有什么办法吗, maven好像并不可以用

[回复](javascript:;)

[用户5610649](https://cloud.tencent.com/developer/user/5610649)回复[用户4626684](https://cloud.tencent.com/developer/user/4626684)

2019-06-13

maven只是系统帮你自动构建，不需要自己导包而已，应该没有什么区别，我用gradle是可以的

[回复](javascript:;)

[用户4626684](https://cloud.tencent.com/developer/user/4626684)回复[用户5610649](https://cloud.tencent.com/developer/user/5610649)

2019-06-13

主要是包和包之间有很多互相依赖的关系，我用的lib的方式好像只能把依赖手动加进来，不知道Gradle是怎么用的呢，就像maven那样可以把依赖都管理起来吗？

[回复](javascript:;)

[展开剩余 1 条评论](javascript:;)

[晴天依旧](https://cloud.tencent.com/developer/user/3938001)

2018-11-18

很详细了，感谢博主的分享