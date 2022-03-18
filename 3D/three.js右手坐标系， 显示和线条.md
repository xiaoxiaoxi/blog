# [three.js右手坐标系， 显示和线条](https://www.cnblogs.com/Yimi/p/6007811.html)

### 1、右手坐标系

Threejs使用的是右手坐标系，这源于opengl默认情况下，也是右手坐标系。下面是右手坐标系的图例，如果对这个概念不理解，可以百度一下，我保证你伸出手比划的那一瞬间你就明白了，如果不明白请给作者留言，我会尽快补上关于坐标系的知识。![three.js坐标系](http://www.hewebgl.com/attached/image/20130515/20130515134934_11.jpg)

图中右边那个手对应的坐标系，就是右手坐标系。在Threejs中，坐标和右边的坐标完全一样。x轴正方向向右，y轴正方向向上，z轴由屏幕从里向外。

## 5、线条的深入理解

 

在Threejs中，一条线由点，材质和颜色组成。

点由THREE.Vector3表示，Threejs中没有提供单独画点的函数，它必须被放到一个THREE.Geometry形状中，这个结构中包含一个数组vertices，这个vertices就是存放无数的点（THREE.Vector3）的数组。这个表示可以如下图所示：![three.js向量](http://www.hewebgl.com/attached/image/20130515/20130515135032_174.png)

为了绘制一条直线，首先我们需要定义两个点，如下代码所示：

var p1 = new THREE.Vector3( -100, 0, 100 );

var p2 = new THREE.Vector3( 100, 0, -100 );

请大家思考一下，这两个点在坐标系的什么位置，然后我们声明一个THREE.Geometry，并把点加进入，代码如下所示：

var geometry = new THREE.Geometry();

geometry.vertices.push(p1);

geometry.vertices.push(p2);

geometry.vertices的能够使用push方法，是因为geometry.vertices是一个数组。这样geometry 中就有了2个点了。

然后我们需要给线加一种材质，可以使用专为线准备的材质，THREE.LineBasicMaterial。

最终我们通过THREE.Line绘制了一条线，如下代码所示:

var line = new THREE.Line( geometry, material, THREE.LinePieces );

ok，line就是我们要的线条了。

 

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>Three框架</title>
        <script src="libs/Three.js"></script>
        <style type="text/css">
            div#canvas-frame {
                border: none;
                cursor: pointer;
                width: 100%;
                height: 600px;
                background-color: #EEEEEE;
            }

        </style>
        <script>
            var renderer;
            function initThree() {
                width = document.getElementById('canvas-frame').clientWidth;
                height = document.getElementById('canvas-frame').clientHeight;
                renderer = new THREE.WebGLRenderer({
                    antialias : true
                });
                renderer.setSize(width, height);
                document.getElementById('canvas-frame').appendChild(renderer.domElement);
                renderer.setClearColor(0xFFFFFF, 1.0);
            }

            var camera;
            function initCamera() {
                camera = new THREE.PerspectiveCamera(45, width / height, 1, 10000);
                camera.position.x = 0;
                camera.position.y = 1000;
                camera.position.z = 0;
                camera.up.x = 0;
                camera.up.y = 0;
                camera.up.z = 1;
                camera.lookAt({
                    x : 0,
                    y : 0,
                    z : 0
                });
            }

            var scene;
            function initScene() {
                scene = new THREE.Scene();
            }

            var light;
            function initLight() {
                light = new THREE.DirectionalLight(0xFF0000, 1.0, 0);
                light.position.set(100, 100, 200);
                scene.add(light);
            }

            var cube;
            function initObject() {
                var geometry = new THREE.Geometry();
                geometry.vertices.push( new THREE.Vector3( - 500, 0, 0 ) );//在x轴上定义两个点p1(-500,0,0)
                geometry.vertices.push( new THREE.Vector3( 500, 0, 0 ) );//p2(500,0,0)

                for ( var i = 0; i <= 20; i ++ ) {//这两个点决定了x轴上的一条线段，将这条线段复制20次，分别平行移动到z轴的不同位置，就能够形成一组平行的线段。

                    var line = new THREE.Line( geometry, new THREE.LineBasicMaterial( { color: 0x000000, opacity: 0.2 } ) );
                    line.position.z = ( i * 50 ) - 500;
                    scene.add( line );

                    var line = new THREE.Line( geometry, new THREE.LineBasicMaterial( { color: 0x000000, opacity: 0.2 } ) );
                    line.position.x = ( i * 50 ) - 500;
                    line.rotation.y = 90 * Math.PI / 180; //  旋转90度
                    scene.add( line );
//将p1p2这条线先围绕y轴旋转90度，然后再复制20份，平行于z轴移动到不同的位置，也能形成一组平行线。
                }
            }

            function threeStart() {
                initThree();
                initCamera();
                initScene();
                initLight();
                initObject();
                renderer.clear();
                renderer.render(scene, camera);
            }

        </script>
    </head>

    <body onload="threeStart();">
        <div id="canvas-frame"></div>
    </body>
</html>
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

![img](https://images2015.cnblogs.com/blog/733346/201610/733346-20161028144907875-241402447.png)

 