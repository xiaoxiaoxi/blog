![如何在threejs中制作UI元素](https://pica.zhimg.com/v2-35187c5736b881d1ab7f4923f0188685_1440w.jpg?source=172ae18b)

# 如何在threejs中制作UI元素

[![林红旭 Leo](https://pic1.zhimg.com/v2-ad199ee5ceffcdfef95ff778bcda0ae2_xs.jpg?source=172ae18b)](https://www.zhihu.com/people/lin-hong-xu-leo)

[林红旭 Leo](https://www.zhihu.com/people/lin-hong-xu-leo)[](https://www.zhihu.com/question/48510028)

IKEA宜家 Webgl前端图形岗

20 人赞同了该文章

我们在很多场景需要使用类似2D UI的效果，比如游戏的小地图啊，瞄准啊，标注啊，地图上的定点啊等等。这篇，我们来讲讲怎么制作一个3D场景的2D UI元素显示效果。

首先，我们来分析分析需求。一般来说，我们的UI元素分为一下几种情况。

1. 固定屏幕位置，不随3D物体移动。类似cs中的小地图，武器装备箱等UI元素。
2. 跟随3D物体的UI展示，类似标签，游戏人物头顶的血条，设备监控的报警提示等。

分析完使用情况后，我们来分别聊聊每种情况的具体实现。

## 固定屏幕位置的2D UI展示

对于固定屏幕位置的2D UI展示，我建议在web上就直接使用html的DOM标签实现。使用决对定位的DIV，重叠在渲染Canvas上。例如下图所示的这种出现在固定位置的UI。其实本质和普通网页的绝对定位`absolute`UI没有什么区别，放心大胆的使用html元素实现，是最简单直接的方式，而且对于交互事件等处理，完全和普通html元素一样，并没有额外的学习、开发成本。



![img](https://pic1.zhimg.com/80/v2-d05d1f58f0d3854ca34339128ce14268_1440w.jpg)



## 跟随3D的UI元素

对于跟随3D的UI元素，首先我们看看下图中的这种提示，一般用来在3D场景中展示尺寸等信息。对于这类信息的展示。我的建议是使用canvas2D的绘图API绘制相关的信息，然后当做贴图`CanvasTexture`，直接贴在面片`Plane`的材质贴图上进行展示。这里，其实并没有“跟随”的概念，因为我们只是在三维场景里面加入了一个三维面片，由于共享三维坐标系的原因，所以ui与三维物体的相对位置是保持一致的。我们对场景统一缩放旋转的时候，作为场景的一部分，自然会跟着一起。

![img](https://pic1.zhimg.com/80/v2-9f74373ae957cd838b48a185568cc918_1440w.jpg)



**一直朝向相机** 更进一步，我们还有一些需求，是这种标签本身并不在场景内，只是做信息提示用。这类标签需要一直面向相机。我们称之为“billboard”广告牌模式。在Three.js中，我们使用`Sprite`类来实现这类广告牌模式的展示。

```text
var spriteMap = new THREE.TextureLoader().load( "sprite.png" );
var spriteMaterial = new THREE.SpriteMaterial( { map: spriteMap } );
var sprite = new THREE.Sprite( spriteMaterial );
scene.add( sprite );
```

展示的内容，我们可以使用一张贴图，或者从canvas创建一个`CanvasTexture`



![img](https://pic2.zhimg.com/80/v2-40ceeb1f949b9142a93599f686dda999_1440w.jpg)





![img](https://pic1.zhimg.com/80/v2-61d24ad874aa99c3a480de865ea93a88_1440w.jpg)



**缩放尺寸不变**

需求进一步升级了，客户说标签如果随着物体缩放，会导致场景很小的时候，标签提示不明显。客户想让场景缩放，当时提示标签不缩放。幸好threejs中的`SpriteMaterial`已经内置了`sizeAttenuation`属性，可以设置不随缩放改变尺寸。

**不被遮挡** 如下图所示，使用Sprite的方案经常还会碰到被遮挡，甚至插入到其他mesh中的情况。造成视觉上的错误。



![img](https://pic2.zhimg.com/80/v2-13fb305676bfa07560a2e45391f045a1_1440w.jpg)





![img](https://pic4.zhimg.com/80/v2-8e99435d8c572ee77aabc8bf398f8b87_1440w.jpg)



我可以设置Material的`depthWrite`属性设置为false，`depthWrite`为false，这样当前的元素就不会写入深度信息，且不参与深度测试。效果就是会展示在所有三维场景的最前面。

**换个思路用2D?**

hud显示的好处，无论你的场景缩放的多大多小，标注会一直不变。足够引起大家的重视。你看百度地图上的icon，无论地图缩放层级多大，上面的图标尺寸都是一样大的。除了直接在三维场景中加入Sprite之外其实我们还有一种比较简单的办法，就是直接在html层中加入一个div，在里面操作dom标签，直接显示，这样div层的显示不会受到3d场景的缩放影响。但是这个解决方案需要解决一个核心的问题，如何将一个3d物体的三维坐标信息转换为屏幕显示的2d屏幕坐标。 在three.js中`Vector3`提供了一个`project(camera)`方法，可以将一个三维的点投射到屏幕坐标。但是webgl的屏幕坐标与Canvas的坐标不同，需要做一次转化。



![img](https://pic1.zhimg.com/80/v2-34206056a62572633a44a923e4d7394c_1440w.jpg)



```text
let glScreen = position3D.project(this.camera);
let widthHalf = 0.5 * renderer.domElement.width;
let heightHalf = 0.5 * renderer.domElement.height;
let positionX = (glScreen.x * widthHalf) + widthHalf;
let positionY = -(glScreen.y * heightHalf) + heightHalf;
```

通过以上代码我们就可以将3d物体的坐标转换成2d的屏幕坐标 显示的代码非常简单直接指定dom元素的`style`的`left`、`top`就可以了

```text
document.getElementById("alarm").style.left = (positionX - 16) + 'px';
document.getElementById("alarm").style.top = (positionY - 16) + 'px';
```

这里减掉的数值是图片的大小，为了将图片的中间显示在左边上。还有一个性能优化的地方，就是我们最好不要在render的主循环中每次更新坐标，而是在场景发生变化后做坐标更新，这样计算量会小很多。这里我们只需监听OrbitControls的start和end方法就好，settimeout,cleartimeout一起使用，防止事件多次执行。

```text
var controls = new THREE.OrbitControls(camera, renderer.domElement);
    controls.addEventListener('end', function () {
        refreshLedPositionTimer = setTimeout(doRefreshLedPosition, 800)
    });


    controls.addEventListener('start', function () {
        clearTimeout(refreshLedPositionTimer);
        document.getElementById("alarm").style.display = "none";
    });
```

这样我们在鼠标开始改变场景的时候隐藏标识，停止后重新计算坐标，显示标识。

![img](https://pic3.zhimg.com/80/v2-80fed41437c43f7a6a4b80b08476428e_1440w.jpg)



发布于 2020-05-28 14:07

[WebGL](https://www.zhihu.com/topic/19573864)

[three.js](https://www.zhihu.com/topic/20024068)

[GUI设计](https://www.zhihu.com/topic/19703816)