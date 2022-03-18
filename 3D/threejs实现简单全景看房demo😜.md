# threejs实现简单全景看房demo😜

[![img](https://p9-passport.byteacctimg.com/img/user-avatar/e883ad00f4c080eae18ebdb3c35aa9d8~300x300.image)](https://juejin.cn/user/4274499823866622)

[半个糯米鸡 ![lv-2](https://lf3-cdn-tos.bytescm.com/obj/static/xitu_juejin_web/f597b88d22ce5370bd94495780459040.svg)](https://juejin.cn/user/4274499823866622)

2021年12月31日 11:51 · 阅读 2532

关注

![threejs实现简单全景看房demo😜](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/847b4f4af48142959e50598ebca24092~tplv-k3u1fbpfcp-zoom-crop-mark:1304:1304:1304:734.awebp?)

各位大家好😊，最近一直在学习 **threejs** ，在学习过程中不断进步，在将来我会不断完善我的 **threejs** 案例库，希望能在学习路上帮到大家🌹

接下来为各位介绍的是一个全景看房的demo，我们先上地址：

- 源码地址：[github.com/ljnMeow/360…](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2FljnMeow%2F360-house-viewing.git)
- 预览地址：[ljnmeow.github.io/360-house-v…](https://link.juejin.cn/?target=https%3A%2F%2Fljnmeow.github.io%2F360-house-viewing%2Fdist)
- 全景图切割工具：[matheowis.github.io/HDRI-to-Cub…](https://link.juejin.cn/?target=https%3A%2F%2Fmatheowis.github.io%2FHDRI-to-CubeMap%2F)

# 前言

**threejs** 是 **javascript** 编写的一个 **WebGL** 第三方库。在 **threejs** 中，我们通过 **Scene(场景)** 、 **Camera(相机)** 和 **Renderer(渲染器)** 来实现一个3d的场景，然后往里面添加各种光源、物体等等，形成一个3d世界。

## threejs支持程度

因为 **threejs** 是基于 **webgl** 写的，所以我们主要看设备是否支持 **webgl** 。据我所知目前主流最新版本的设备、浏览器都支持 **webgl**，但如果客服要在一些早期的设备上跑，例如某些超大屏大屏监控系统，跑这个的设备可能是早期的 **IE** 并且无法升级。我们还是需要权衡下早期 **IE** 和 安卓、苹果设备是否支持 **webgl**， 详情可见下图：

![image.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/73c7afd6ff494c28b1618909952636fc~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

# 基本介绍

要实现3d图形的展示，大致是以下思路：

- 创建三维场景(Scene)
- 选择视觉点并确认视觉位置角度(Camera)
- 添加物体供观察
- 渲染场景(Renderer)

## Scene

场景是我们所有物体的容器，通俗来讲就相当于我们的世界

## Camera

相机是我们这个世界的观察者，使用右手坐标系定位

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bd8fb7ed0d554a7a9c726fc869acc52c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

**threejs** 常用的相机有两种，分别是 **正交投影相机(OrthographicCamera)** 和 **透视投影相机(PerspectiveCamera)** ，下面是我对这两种方式的理解，错了请各位大佬指点我一下🤞

### 正交投影相机(OrthographicCamera)

正交投影是一种相对简单的投影模式，我们可以把该模式看作看作一个长方形矩形，总共有6个面。该模式的特点是无论出于矩形中的哪个位置，其投影的大小都是一样的，通俗理解就是该模式跟常生活中的视觉效果不一样。我们平时看物体是远小近大，而该模式下展示的物体无论物体距离相机距离远或者近，在最终渲染的图片中物体的大小都保持不变。通过下面图片能清楚看到，相机视觉中的物体投放到进平面，然后近平面中的物体渲染到远平面也就是屏幕中，并且无论投放在哪一面，物体的大小都不变。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ee9400e7e1a64b7491b5aad97dbb6704~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

### 透视投影相机(PerspectiveCamera)

透视投影的视觉效果呈现一个锥形，该模式就是我们现实世界中的视觉体现。该模式的特点是物体远小近大。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/792dce4e31a14ab2bd0b5bb9026f3700~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

相机效果体验地址在官方demo中有：[threejs.org/examples/#w…](https://link.juejin.cn/?target=https%3A%2F%2Fthreejs.org%2Fexamples%2F%23webgl_camera)

## Renderer

渲染器渲染我们精心制作的场景

# 进入正题

根据我的了解目前常用于实现全景看房效果的有两种，分别是 **天空盒(skyBox)** 和 **全景图片贴图** ，我这个demo使用的是后者。

## 实现方式

### skyBox

**skyBox** 方法是最容易理解的，在我们身处的场景内，无非就是6个面，上下、前后、左右。将这6个面的视觉处理成图片就得到6张不同方向视觉的图片。

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1e143d8cea7f466ab4f2917116551a84~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

我们将6个视觉的图片贴到立方体的6个面，可以得到一个房间。

```
initContent() {
  let picList = ["left", "right", "top", "bottom", "front", "back"];
  let boxGeometry = new THREE.BoxGeometry(10, 10, 10);
  let boxMaterials = [];
  picList.forEach((item) => {
    let texture = new THREE.TextureLoader().load(
      require(`@/assets/image/${item}.png`)
    );
    boxMaterials.push(new THREE.MeshBasicMaterial({ map: texture }));
  });
  this.box = new THREE.Mesh(boxGeometry, boxMaterials);
  this.scene.add(this.box);
},
复制代码
```

![屏幕录制2021-12-30 下午11.00.31.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/77fed458999b4348bb1fb5bf5794cf27~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

将视觉移到立方体中心，并让贴图内翻转一下，就能实现全景看房

```
this.box.geometry.scale(10, 10, -10);
复制代码
```

![屏幕录制2021-12-30 下午11.11.50.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/183faf80bd05437fac28de39c99985f2~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

### 全景图贴图

全景图贴图这种方式我认为是简单而且效果最好的一种。写之前需要一张全景图片，这个用单反的全景模式就能拍一张

![livingRoom.jpg](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/d07d7698264f42028dc226077995faae~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

**threejs** 添加一个球体。并把全景图作为贴图贴到球体上，得到的效果如下：

```
initContent() {
  let sphereGeometry = new THREE.SphereGeometry(16, 50, 50);
  let texture = new THREE.TextureLoader().load(require("@/assets/image/livingRoom.jpg"));
  let sphereMaterial = new THREE.MeshBasicMaterial({ map: texture });
  this.sphere = new THREE.Mesh(sphereGeometry, sphereMaterial);
  this.scene.add(this.sphere);
},
复制代码
```

![轻映录屏-2021-12-31-10-11-37.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fcb9b952fe3449d29b8f552b744eaf55~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

同样，把视觉放球内，贴图反转。

```
sphereGeometry.scale(16, 16, -16);
复制代码
```

![轻映录屏-2021-12-31-10-20-58.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/8178cb958117495f858b5ef385968ed3~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

## 添加标签

我们现在已经实现全景看房了，接下来给一些物体添加说明标签，我这边的标签分两种，一种点击能够进入下一个房间，一种是弹出信息框。先看效果：

![轻映录屏-2021-12-31-10-32-16.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/b48465811db345dd9aa12bb3ff7a239d~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

下面看看我的数据结构

```
dataList: [
    {
        image: require("@/assets/image/livingRoom.jpg"), // 场景贴图
        tipsList: [ // 标签数据
            {
                position: { x: -200, y: -4, z: -147 }, // 标签位置
                content: { // 标签内容
                    title: "进入厨房", // 标题
                    text: "", // 文本内容
                    image: 1, // 场景贴图的下标，对应dataList下标
                    showTip: false, // 是否展示弹出框
                    showTitle: true, // 是否展示提示标题
                },
            },
            {
                position: { x: -100, y: 0, z: -231 },
                content: {
                    title: "信息点2",
                    text: "77989",
                    showTip: true,
                    showTitle: false,
                },
            },
            {
                position: { x: 150, y: -50, z: -198 },
                content: {
                    title: "信息点3",
                    text: "qwdcz",
                    showTip: true,
                    showTitle: false,
                },
            },
            {
                position: { x: 210, y: 11, z: -140 },
                content: {
                    title: "信息点4",
                    text: "大豆食心虫侦察十大大苏打大大大大大大大",
                    showTip: true,
                    showTitle: false,
                },
            },
            {
                position: { x: 208, y: -12, z: 140 },
                content: {
                    title: "信息点5",
                    text: "eq",
                    showTip: true,
                    showTitle: false,
                },
            },
            {
                position: { x: 86, y: -9, z: 236 },
                content: {
                    title: "进入房间",
                    text: "",
                    showTip: false,
                    showTitle: true,
                },
            },
        ],
    },
    {
        image: require("@/assets/image/kitchen.jpg"),
        tipsList: [
            {
                position: { x: -199, y: -24, z: 145 },
                content: {
                    title: "进入大厅",
                    text: "",
                    image: 0,
                    showTip: false,
                    showTitle: true,
                },
            },
        ],
    },
],
复制代码
```

往场景中添加标签，得到如下效果。

```
addTipsSprite(index = 0) {
  let tipTexture = new THREE.TextureLoader().load(
    require("@/assets/image/tip.png")
  );
  let material = new THREE.SpriteMaterial({ map: tipTexture });
  this.tipsSpriteList = [];
  this.dataList[index].tipsList.forEach((item) => {
    let sprite = new THREE.Sprite(material);
    sprite.scale.set(10, 10, 10);
    sprite.position.set(item.position.x, item.position.y, item.position.z); // 设置标签位置
    sprite.content = item.content; // 设置标签内容
    this.tipsSpriteList.push(sprite); // 储存标签
    this.scene.add(sprite); // 添加到场景中
  });
},
复制代码
```

![轻映录屏-2021-12-31-10-52-05.gif](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/346e25b0db2946239a2df5973497e21a~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

接下来实现鼠标移入，内容弹出效果

```
// html
<div class="tooltip-box" :style="tooltipPosition" ref="tooltipBox">
  <div class="container">
    <div class="title">标题：{{ tooltopContent.title }}</div>
    <div class="explain">说明：{{ tooltopContent.text }}</div>
  </div>
</div>
<p class="title-text" ref="titleBox" :style="titlePosition">
  {{ tooltopContent.title }}
</p>
复制代码
// data
tooltipPosition: { // 初始化位置全部在屏幕之外
    top: "-100%",
    left: "-100%",
},
titlePosition: {
    top: "-100%",
    left: "-100%",
},
tooltopContent: {}, // 展示的内容
复制代码
// method
onMousemove(e) {
  e.preventDefault();
  let element = this.$refs.threeDBox;
  let raycaster = new THREE.Raycaster();
  let mouse = new THREE.Vector2();
  // 通过鼠标点击的位置计算出raycaster所需要的点的位置，以屏幕中心为原点，值的范围为-1到1.
  mouse.x = (e.clientX / element.clientWidth) * 2 - 1;
  mouse.y = -(e.clientY / element.clientHeight) * 2 + 1;
  raycaster.setFromCamera(mouse, this.camera);
  // 将标签精灵数据放进来做视线交互
  let intersects = raycaster.intersectObjects(this.tipsSpriteList, true); 
  // 视线穿过集合选择最前面的一个
  if (intersects.length > 0) {
    // 将标签的空间坐标转屏幕坐标，通过计算赋给元素的top、left
    let elementWidth = element.clientWidth / 2;
    let elementHeight = element.clientHeight / 2;
    let worldVector = new THREE.Vector3(
      intersects[0].object.position.x,
      intersects[0].object.position.y,
      intersects[0].object.position.z
    );
    let position = worldVector.project(this.camera);
    this.tooltopContent = intersects[0].object.content;
    if (intersects[0].object.content.showTip) {
      let left = Math.round(
        elementWidth * position.x +
          elementWidth -
          this.$refs.tooltipBox.clientWidth / 2
      );
      let top = Math.round(
        -elementHeight * position.y +
          elementHeight -
          this.$refs.tooltipBox.clientHeight / 2
      );
      this.tooltipPosition = {
        left: `${left}px`,
        top: `${top}px`,
      };
    } else if (intersects[0].object.content.showTitle) {
      let left = Math.round(
        elementWidth * position.x +
          elementWidth -
          this.$refs.titleBox.clientWidth / 2
      );
      let top = Math.round(-elementHeight * position.y + elementHeight);
      this.titlePosition = {
        left: `${left}px`,
        top: `${top}px`,
      };
    }
  } else {
    // 鼠标移出去隐藏所有
    this.handleTooltipHide(e);
  }
},
handleTooltipHide(e) {
  e.preventDefault();
  this.tooltipPosition = {
    top: "-100%",
    left: "-100%",
  };
  this.titlePosition = {
    top: "-100%",
    left: "-100%",
  };
  this.tooltopContent = {};
},
复制代码
// mounted
this.renderer.domElement.addEventListener(
  "mousemove",
  this.onMousemove,
  false
);
this.$refs.tooltipBox.addEventListener(
  "mouseleave",
  this.handleTooltipHide,
  false
);
复制代码
```

最终得到效果：

![轻映录屏-2021-12-31-11-08-13.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fa07d85bcd9f4053992e977e01f3cad1~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

## 场景切换

全景看房总不能一直看一个房间，所以我们还需要实现点击切换场景功能。直接codeing...

```
changeContentAndtips(index) {
  // 清除场景数据内所有的精灵标签
  this.scene.children = this.scene.children.filter(
    (item) => String(item.type) !== "Sprite"
  );
  // 储存数组置空
  this.tipsSpriteList = [];
  // 重新加载贴图，这边应用gasp做一个简单的过渡动画，将透明度从0 ~ 1
  let texture = new THREE.TextureLoader().load(this.dataList[index].image);
  let sphereMaterial = new THREE.MeshBasicMaterial({
    map: texture,
    transparent: true,
    opacity: 0,
  });
  this.sphere.material = sphereMaterial;
  gsap.to(sphereMaterial, { transparent: true, opacity: 1, duration: 2 });
  // 手动更新投影矩阵
  this.camera.updateProjectionMatrix();
  // 添加当前场景标签
  this.addTipsSprite(index);
},
onMouseClick(e) {
  e.preventDefault();
  let element = this.$refs.threeDBox;
  let raycaster = new THREE.Raycaster();
  let mouse = new THREE.Vector2();
  mouse.x = (e.clientX / element.clientWidth) * 2 - 1;
  mouse.y = -(e.clientY / element.clientHeight) * 2 + 1;
  raycaster.setFromCamera(mouse, this.camera);
  let intersects = raycaster.intersectObjects(this.tipsSpriteList, true);
  if (intersects.length > 0 && intersects[0].object.content.showTitle) {
    this.changeContentAndtips(intersects[0].object.content.image);
    this.handleTooltipHide(e);
  }
},
复制代码
```

最终得到完整效果如下图：

![轻映录屏-2021-12-31-11-18-19.gif](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/af5ec22cb36043b0973bc095df78c8d7~tplv-k3u1fbpfcp-zoom-in-crop-mark:1304:0:0:0.awebp?)

# 总结

在这个demo中有一些细节问题我处理的不是很好，例如加载时因为贴图加载慢黑屏(这是因为贴图太大，优化时可加入等待动画)，还有就是加载顺序没处理好，场景贴图还没加载完标签已经进来了。

在不断学习 **threejs** 的过程中，感觉还是挺有趣，看着别人炫酷的3D效果和智慧城市感觉好强，也感到自己的不足。趁着这段时间公司有项目需要用 **threejs** 能够光明正大摸鱼学习，努力冲啊💪

最后希望这篇文章能帮到各位❤今天是2021最后一天，祝各位大佬今天摸鱼，明年年年有余😁