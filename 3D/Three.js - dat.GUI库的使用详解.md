# Three.js - dat.GUI库的使用详解

2017-10-03发布：hangge阅读：28558

## 一、基本介绍

### 1，什么是 dat.GUI?

**dat.GUI** 是一个轻量级的图形用户界面库（**GUI** 组件），使用这个库可以很容易地创建出能够改变代码变量的界面组件。

- **GitHub** 主页：https://github.com/dataarts/dat.gui

### 2，使用步骤

（1）首先在页面的 **<head>** 标签中添加这个库。

```
<script type=``"text/javascript"` `src=``"../libs/dat.gui.js"``></script>
```


（2）定义一个 **JavaScript** 对象（这里假设叫做 **controls**），该对象将保存希望通过 **dat.GUI** 改变的属性。

```
var controls = new function () {
    this.rotationSpeed = 0.02;
    //......
};
```


（3）接下来需要将这个 **JavaScript** 对象传递给 **dat.gui** 对象，并设置各个属性的取值范围。

```
var gui = new dat.GUI();
gui.add(controls, 'rotationSpeed', 0, 0.5);
//......
```


（4）最后当用户对 **dat.GUI** 控件进行操作时，**controls** 里的属性值也会同步修改。我们在程序中直接引用这个属性值就好了。

### 3，简单的使用样例

（1）效果图

页面打开后场景中央会有一个不断旋转的立方体。默认旋转速度是 **0.02**。

我们使用 **dat.GUI** 添加一个控制面板，里面只有一个控制项，用于实时修改方块的旋转速度（可以填值，也可以左右拖动调整）

  [![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/201709051033085824.png)](https://www.hangge.com/blog/cache/detail_1785.html#)  [![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090510332330436.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

（2）样例代码



```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>hangge.com</title>
    <script type="text/javascript" src="../libs/three.js"></script>
    <script type="text/javascript" src="../libs/dat.gui.js"></script>
    <style>
        body {
            margin: 0;
            overflow: hidden;
        }
    </style>
</head>
<body>
 
<!-- 作为Three.js渲染器输出元素 -->
<div id="WebGL-output">
</div>
 
<!-- 第一个 Three.js 样例代码 -->
<script type="text/javascript">
 
    //网页加载完毕后会被调用
    function init() {
 
        //创建一个场景（场景是一个容器，用于保存、跟踪所要渲染的物体和使用的光源）
        var scene = new THREE.Scene();
 
        //创建一个摄像机对象（摄像机决定了能够在场景里看到什么）
        var camera = new THREE.PerspectiveCamera(45,
          window.innerWidth / window.innerHeight, 0.1, 1000);
 
        //设置摄像机的位置，并让其指向场景的中心（0,0,0）
        camera.position.x = -30;
        camera.position.y = 40;
        camera.position.z = 30;
        camera.lookAt(scene.position);
 
        //创建一个WebGL渲染器并设置其大小
        var renderer = new THREE.WebGLRenderer();
        renderer.setClearColor(new THREE.Color(0xEEEEEE));
        renderer.setSize(window.innerWidth, window.innerHeight);
 
        //创建一个立方体
        var cubeGeometry = new THREE.BoxGeometry(10, 10, 10);
        //将线框（wireframe）属性设置为true，这样物体就不会被渲染为实物物体
        var cubeMaterial = new THREE.MeshLambertMaterial({color: 0xff0000});
        var cube = new THREE.Mesh(cubeGeometry, cubeMaterial);
        cube.castShadow = true;
 
        //设置立方体的位置
        cube.position.x = -4;
        cube.position.y = 3;
        cube.position.z = 0;
 
        //将立方体添加到场景中
        scene.add(cube);
 
        //创建点光源
        var spotLight = new THREE.SpotLight(0xffffff);
        spotLight.position.set(-40, 60, -10);
        spotLight.castShadow = true;
        scene.add(spotLight);
 
        //将渲染的结果输出到指定页面元素中
        document.getElementById("WebGL-output").appendChild(renderer.domElement);
 
        //存放有所有需要改变的属性的对象
        var controls = new function () {
            this.rotationSpeed = 0.02;
        };
 
        //创建dat.GUI，传递并设置属性
        var gui = new dat.GUI();
        gui.add(controls, 'rotationSpeed', 0, 0.5);
 
        //渲染场景
        render();
 
        //渲染场景
        function render() {
            //选装立方体
            cube.rotation.x += controls.rotationSpeed;
            cube.rotation.y += controls.rotationSpeed;
            cube.rotation.z += controls.rotationSpeed;
 
            //通过requestAnimationFrame方法在特定时间间隔重新渲染场景
            requestAnimationFrame(render);
            //渲染场景
            renderer.render(scene, camera);
        }
    }
 
    //确保init方法在网页加载完毕后被调用
    window.onload = init;
</script>
</body>
</html>
```



## 二、各种类型的控件

**dat.GUI** 会根据我们设置的属性类型来渲染使用不同的控件。

### 1，数字类型（Number）

```
//存放有所有需要改变的属性的对象
var controls = new function () {
    this.rotationSpeed = 0.02;
};
```



（1）如果没有设置限制条件，则为一个 **input** 输入框。

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516075546391.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var gui = new dat.GUI();
gui.add(controls, 'rotationSpeed');
```



（2）可以设置最小值最大值范围，则显示为 **slider** 滑块组件（当然右侧还是有 **input** 输入）

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516082747198.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var gui = new dat.GUI();
gui.add(controls, 'rotationSpeed', 0, 0.5);
```


（3）还可以只单独限制最小值或者最大值，这个同样为一个 **input** 输入框。

```
var gui = new dat.GUI();
gui.add(controls, 'rotationSpeedX').min(0);
gui.add(controls, 'rotationSpeedY').max(10);
```


（4）可以配合 **step** 限制步长。

```
var gui = new dat.GUI();
gui.add(controls, 'rotationSpeedX').step(0.5);
gui.add(controls, 'rotationSpeedY', 0, 3).step(0.5);
gui.add(controls, 'rotationSpeedZ').max(10).step(0.5);
```



（5）如果数字只是有限的几种固定值，那还可以使用下拉框的形式。

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516121766745.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var gui = new dat.GUI();
gui.add(controls, 'rotationSpeed', { Stopped: 0, Slow: 0.02, Fast: 5 });
```



### 2，字符串类型（String）

（1）默认情况下就是一个 **input** 输入框。

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516131473957.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var controls = new function () {
    this.site = "hangge.com"
};
 
var gui = new dat.GUI();
gui.add(controls, 'site');
```



（2）只是有限的几种固定值，那还可以使用下拉框的形式。

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516134079438.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var controls = new function () {
    this.site = "hangge.com"
};
 
var gui = new dat.GUI();
gui.add(controls, 'site', [ 'google.com', 'hangge.com', '163.com' ]);
```



### 3，布尔类型（Boolean ）

使用复选框（**Checkbox**）的形式控制。

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516140729780.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var controls = new function () {
    this.visible = true
};
 
var gui = new dat.GUI();
gui.add(controls, 'visible');
```



### 4，自定义函数（Function）

使用按钮（**button**）的形式控制，点击按钮会调用相应的方法。

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516143745228.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var controls = new function () {
    this.hello = function() {
      alert("欢迎访问 hangge.com");
    }
};
 
var gui = new dat.GUI();
gui.add(controls, 'hello');
```



### 5，颜色值

**dat.GUI** 一共提供了 **4** 种类型颜色输入控制：**CSS**、**RGB**、**RGBA**、**Hue**（注意：颜色使用 **addColor** 方法添加控件）

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516150515831.png)](https://www.hangge.com/blog/cache/detail_1785.html#)

```
var controls = new function () {
    this.color0 = "#ffae23"; // CSS string
    this.color1 = [0, 128, 255]; // RGB array
    this.color2 = [0, 128, 255, 0.3]; // RGB with alpha
    this.color3 = {h: 350, s: 0.9, v: 0.3}; // Hue, saturation, value
};
 
var gui = new dat.GUI();
gui.addColor(controls, 'color0');
gui.addColor(controls, 'color1');
gui.addColor(controls, 'color2');
gui.addColor(controls, 'color3');
```



## 三、事件监听

对于面板中的每一个控制项，我们都可以设置 **onChange** 和 **onFinishChange** 监听事件。

（1）样例代码

```
var controls = new function () {
    this.speed = 1;
};
 
var gui = new dat.GUI();
var speedController = gui.add(controls, 'speed', 0, 5);
 
//对应控制项值改变时响应（比如拖动滑块过程中）
speedController.onChange(function(value) {
  console.log("onChange:" + value)
});
 
//对应控制项值修改完毕响应
speedController.onFinishChange(function(value) {
  console.log("onFinishChange" + value)
});
```


（2）我们拖动滑块改变值，控制台输出如下：

[![原文:Three.js - dat.GUI库的使用详解：上（实现图形控制界面）](https://www.hangge.com/blog_uploads/201709/2017090516275522266.png)](https://www.hangge.com/blog/cache/detail_1785.html#)



## 四、设置控制项标签文字

默认情况下每个控制项左侧的标签显示的是对应的属性名，我们可以通过 **name** 方法设置成其他的文字（中文也是支持的）

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/201709060910128329.png)](https://www.hangge.com/blog/cache/detail_1786.html#)

```
var controls = new function () {
    this.speed = 1;
};
 
var gui = new dat.GUI();
gui.add(controls, 'speed', 0, 10).name("旋转速度");
```



## 五、控制项分组

如果控制面板上的项目太多，可以考虑将一些功能近似的控制项分到一个分组文件夹中，这样可以让结构更加清晰。

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/2017090516390685468.png)](https://www.hangge.com/blog/cache/detail_1786.html#)

```
var controls = new function () {
    this.rotationSpeed = 0.02;
    this.x = 1;
    this.y = 1;
    this.z = 1;
    this.width = 50;
    this.height = 60;
};
 
var gui = new dat.GUI();
 
//第一个分组
var f1 = gui.addFolder('Position');
f1.add(controls, 'x');
f1.add(controls, 'y');
f1.add(controls, 'z');
 
//第二个分组
var f2 = gui.addFolder('Size');
f2.add(controls, 'width');
f2.add(controls, 'height');
//第二个分组默认打开
f2.open();
```



## 六、存储模式

### 1，开启存储功能模式

（1）使用 **remember** 方法可以开启 **GUI** 的存储模式（而且可以分组存储）

```
var controls = new function () {
    this.speed = 1;
};
 
var gui = new dat.GUI();
gui.remember(controls);
gui.add(controls, 'speed', 0, 5);
```



### 2，存储模式介绍

(1)存储模式开启后效果如下，每个控制项点击“**Revert**”按钮可以还原成默认值。

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/2017090516584644696.png)](https://www.hangge.com/blog/cache/detail_1786.html#)

（2）点击“**Save**”可以将当前面板设置的值保存成默认值。点击“**New**”可以新建一个配置分组。通过下拉框可以切换各个分组（分组切换时控制项的值也会随之改变）。

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/2017090516572318266.png)](https://www.hangge.com/blog/cache/detail_1786.html#)



（3）点击齿轮图标可以看到对应配置分组保存的值。

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/2017090517024990568.png)](https://www.hangge.com/blog/cache/detail_1786.html#)



### 3，初始化时导入分组配置值

我们也可以把之前保存的分组配置数据在初始化时导入。

```
var controls = new function () {
    this.rotationSpeed = 0.02;
    this.speed = 1;
};
 
var gui = new dat.GUI({
  load:{
    "preset": "Default",
    "closed": false,
    "remembered": {
      "Default": {
        "0": {
          "speed": 2.157493649449619
        }
      },
      "Custom1": {
        "0": {
          "speed": 1
        }
      }
    },
    "folders": {}
  }
});
 
gui.remember(controls);
gui.add(controls, 'speed', 0, 5);
```



## 七、获取面板的DOM对象

通过 **gui.domElement** 我们可以获取到控制面板原生 **dom** 对象。比如我们将面板位置改成页面左上角。

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/2017090517190255168.png)](https://www.hangge.com/blog/cache/detail_1786.html#)

```
var controls = new function () {
    this.speed = 1;
};
 
var gui = new dat.GUI();
gui.add(controls, 'speed', 0, 5);
 
gui.domElement.style = 'position:absolute;top:0px;left:0px';
```



## 八、从 GUI 外部控制配置项

如果我们想不通过操作控制面板，而是从外部修改控制项数据。可以让控制项调用 **listen** 方法，这样当我们改变数据时，也会同步到面板里。

（1）样例代码

```
var controls = new function () {
    this.speed = 1;
};
 
var gui = new dat.GUI();
gui.add(controls, 'speed', 0, 10).listen();
 
setInterval(function() {
  controls.speed = Math.random() * 10;
}, 500);
```


（2）可以看到控制面板中 **speed** 项的值每隔 **500ms** 就会自动改变一次

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/2017090517323326985.png)](https://www.hangge.com/blog/cache/detail_1786.html#)



## 九、创建多个 GUI 对象

我们可以通过构造函数 **dat.GUI()** 创建多个 **GUI** 对象，每个对象对应的都是一个独立的控制面板。

（1）样例代码

```
var controls = new function () {
    this.rotationSpeed = 0.01;
    this.x = 0;
    this.y = 0;
    this.z = 0;
};
 
var gui = new dat.GUI();
gui.add(controls, 'x', -10, 10);
gui.add(controls, 'y', -10, 10);
gui.add(controls, 'z', -10, 10);
 
var gui2=new dat.GUI();//创建GUI对象
gui2.domElement.style = 'position:absolute;top:0px;left:0px;width:50px';
gui2.add(controls,'rotationSpeed',{低速: 0.005, 中速: 0.01,高速: 0.1});
```

（2）我们创建两个 **GUI** 对象，第一个位于默认的右上角位置，第二个放置在界面左上角。效果图如下：

[![原文:Three.js - dat.GUI库的使用详解：下（进阶用法）](https://www.hangge.com/blog_uploads/201709/2017090609233382770.png)](https://www.hangge.com/blog/cache/detail_1786.html#)


