# 用three.js绘制一个三维直角坐标系

[![img](https://cdn2.jianshu.io/assets/default_avatar/11-4d7c6ca89f439111aff57b23be1c73ba.jpg)](https://www.jianshu.com/u/f96ad9666bf5)

[呆呆的木木](https://www.jianshu.com/u/f96ad9666bf5)关注

12017.01.17 11:49:15字数 3,177阅读 19,018

Three.js是一个3DJavaScript库，基于右手坐标系，可以创建简单或是比较复杂的三维图形并应用丰富多彩的纹理和材质，可以添加五光十色的光源，可以在3D场景中移动物体或是添加脚本动画，等等。关于three.js这些功能的教程，只要用心去找，还是可以找到不少资料的。然而，却鲜少有绘制坐标系的经验。因此我们今天主要说的是绘制三维坐标系的方法以及问题，也就是网上没找到的资料。下面的教程默认您已经学习了基本的three.js，对three.js有一定的了解。



![img](https://upload-images.jianshu.io/upload_images/2261933-4be23520d672d39f.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/887/format/webp)

三维坐标系最终效果图



------

####  

#### 1.首先，我们引入一些需要js文件，[下载地址](https://link.jianshu.com/?t=https%3A%2F%2Fgithub.com%2Fmrdoob%2Fthree.js%2Ftree%2Fmaster%2Fbuild)  

> <script src="js/three.js"></script>//这个是Three.js引擎的js
>
> <script src="js/Detector.js">/script>//探测器 就是检测当前浏览器是否支持或者开启了WEBGL
>
> <script src="js/Stats.js">/script>//JavaScript性能监控器 监控代码的性能 这里监测动画效果
>
> <script src="js/OrbitControls.js">/script>//鼠标控制旋转的js
>
> <script src="js/THREEx.KeyboardState.js">/script>//这个是保持键盘的当前状态
>
> <script src="js/THREEx.FullScreen.js">/script>//查不到，猜测和全屏控制有关
>
> <script src="js/THREEx.WindowResize.js">/script>//处理窗口大小调整。它将在调整窗口的大小时更新渲染和相机

####  

#### 2.按照教程加上基础的场景，摄像机，渲染器，灯光等，再加上自己需要的功能代码，例如：

> THREEx.WindowResize(renderer, camera);//处理窗口大小调整。
>
> controls = new THREE.OrbitControls( camera, renderer.domElement );//鼠标控制旋转

####  

#### 3.绘制三维坐标

这里就是我们今天要说的核心内容了，由于我当时是希望将左边的三维图形放进一个mesh，因此，下面示例中添加任何物体的方法都是：

> this.mesh.add();

然后在所有物体添加到mesh之后，直接用

> scene.add(mesh);

如果你不需要将左边放进一个mesh的话，可以直接按照教程用：

> scene.add();

**a.添加网格**

GridHelper辅助绘制线条的二维网格。第一个参数是网格大小，第二个参数是网格个数，后面是网格颜色。xxx.position.set( 80,0,80 )为网格的中心点坐标。

> var gridXZ = new THREE.GridHelper(80, 10, 0xEED5B7, 0xEED5B7);
>
> gridXZ.position.set( 80,0,80 );
>
> this.mesh.add(gridXZ);
>
> var gridXY = new THREE.GridHelper(80, 10, 0xEED5B7, 0xEED5B7);
>
> gridXY.position.set( 80,80,0 );
>
> gridXY.rotation.x = Math.PI/2;
>
> this.mesh.add(gridXY);
>
> var gridYZ = new THREE.GridHelper(80, 10, 0xEED5B7, 0xEED5B7);
>
> gridYZ.position.set( 0,80,80 );
>
> gridYZ.rotation.z = Math.PI/2;
>
> this.mesh.add(gridYZ);

**b.添加坐标文字**

three.js没有直接写坐标刻度的方法（也许因为我没有查到），因此，我们采用three.js的文字处理方式，将字显示在需要的坐标，这里我们可以利用循环将刻度值显示出来。

定义字体的材质颜色等信息。其中specular指定该材质的光亮程度及其高光部分的颜色，如果设置成和color属性相同的颜色，则会得到另一个更加类似金属的材质，如果设置成grey灰色，则看起来像塑料；shininess指定高光部分的亮度，默认值为30。

> var materialtext = new THREE.MeshPhongMaterial({
>
> 　　color: 0xEEA2AD,
>
> 　　specular:0xEEA2AD,
>
> 　　shininess:0
>
> });

文字引用方法，下面以x轴坐标刻度为例，y轴和z轴类似，直接在loader.load中添加：

> var loader = new THREE.FontLoader();
>
> loader.load('fonts/helvetiker_regular.typeface.json', function(font) {
>
> 　　for(i=1;i<=10;i++){
>
> 　　　　var x = 160/10*i;
>
> 　　　　var meshtextx = new THREE.Mesh(new THREE.TextGeometry(x, {
>
> 　　　　　　font: font,
>
> 　　　　　　size: 3,
>
> 　　　　　　height: 0.1
>
> 　　　　}), materialtext);
>
> 　　　　meshtextx.position.set(x,0,170);
>
> 　　　　this.mesh.add(meshtextx);
>
> 　　}
>
> });

**c.绘制直线**

细心的朋友们会发现，示例图的外围描了一层边框，那是用直线绘制的，下面是直线的绘制方法，注意，不仅是用于坐标描边，可以用于任何地方，只要你定义了线段坐标。示例：

> var linematerial = new THREE.LineBasicMaterial( { vertexColors: THREE.VertexColors, linewidth: 1.3} );
>
> var color1 = new THREE.Color( 0x000000 ), color2 = new THREE.Color( 0x000000 );
>
> var p1 = new THREE.Vector3( 0, 0, 0 );
>
> var p2 = new THREE.Vector3( 0, 0, 160 );
>
> var geometry = new THREE.Geometry();
>
> geometry.vertices.push(p1);
>
> geometry.vertices.push(p2);
>
> geometry.colors.push( color1, color2 );
>
> var line = new THREE.Line( geometry, linematerial, THREE.LinePieces );
>
> this.mesh.add(line);

**d.添加物体**

现在我们绘制好了坐标轴，可以添加物体了。geometry为物体形状，material为物体材质，两项均是可自定义的：

> this.mesh = new THREE.Object3D();//忘了强调，**这句话要放在所有的this.mesh.add()之前**
>
> var geometry = new THREE.SphereGeometry( 0.3, 32, 16 );
>
> var material = new THREE.MeshLambertMaterial( { color: 0x00ff00 } );
>
> meshpoint = new THREE.Mesh( geometry, material );
>
> meshpoint.position.set(40,40,40);
>
> this.mesh.add(meshpoint);

对于三维坐标系来说，就一个物体太单薄了。我们可以随机添加一些绿色的球形物体：

> var geometry = new THREE.SphereGeometry( 0.3, 32, 16 );
>
> var material = new THREE.MeshLambertMaterial( { color: 0x00ff00 } );
>
> for(i=0;i<2000;i++){
>
> 　　var sjs1=Math.random();
>
> 　　var sjs2=Math.random();
>
> 　　var sjs3=Math.random();
>
> 　　var meshpoint = 'mesh'+i;
>
> 　　meshpoint = new THREE.Mesh( geometry, material );
>
> 　　meshpoint.position.set(160*sjs1,160*sjs2,160*sjs3);
>
> 　　this.mesh.add(meshpoint);
>
> }

**e.添加旁边色度条**

色度条是很多数据分析类图形的必备，它可以根据不同的数值反应不同的颜色，在下载的图形中也许你也可以找到three.js绘制的色度条，但是因为场景灯光等条件相同，色度条会随着三维场景的旋转而进行旋转。我们可以找到两种方法控制旋转：

整个图形不随着鼠标旋转，即类似于静态图，然后正如我在本文开头所说的，将左边图形作为一个mesh，然后在代码中写一个函数，在render中执行，使左边的mesh旋转起来，这个可以实现表面的旋转，但是不可控，会按照代码一直旋转，鼠标无法操控图形。显然这不是我们想要的效果，在此不做举例了，有小伙伴想要的话可以私我要示例代码。

按照三维图形常规来绘制三维图形，鼠标可以操作mesh旋转，可是这样的话色度条也按照鼠标操作旋转起来，怎么办呢？我们也许可以定义一个div，把色度条写在定义的div中，这里可以用css3绘制色度条，效果不错。下面用css3将色度条绘制在定义好的id为colorBar的div中。示例：

> $("#colorBar")
>
> .css({ "height": "30%",
>
> 　　"width":"35px",
>
> 　　"z-index":"2",
>
> 　　"background":"linear-gradient(to top, #0000FF , #00FFFF,#00FF00,#FFFF00,#FF0000)",
>
> 　　"position":"absolute", "top":"30.5%", "right":"15%"
>
> })

这里只绘制了一个色度条，还需要有一些刻度值以及单位等信息，你也同样可以定义一些div，将位置和样式定义好，用js将刻度值写入定义好的div中，不做赘述。

**f.将色度值与球形物体值匹配**

好了，现在我们可以看到示例图片的效果了吧。哎，好像哪里不对，因为图中的球形物体是彩色的，而我们绘制的图形中球形物体只有单薄的绿色。怎么办呢？别急，下面我们将色度条和球形物体的值匹配，为了测试效果，我们将颜色值与三维图形中向上的y轴值匹配显示。

首先我们定义一个数组，存放色度条的刻度值：

> var colorval = [0,40,80,120,160];

然后，再定义一个数组，与色度条的值匹配，其中colors[0]第一个参数为相应的刻度值在色度条中的位置，第二个参数为相应的刻度值对应的颜色，第三个参数是对应的刻度值，以此类推：

> var colors = [ [ 0.0, '0x0000FF',colorval[0]], [ 0.25,'0x00FFFF',colorval[1] ], [ 0.5,'0x00FF00',colorval[2] ], [ 0.75,'0xFFFF00',colorval[3] ], [ 1.0, '0xFF0000' ],colorval[4] ];

下面就可以将色度值和y值做关联咯。我们将色度条看成一个整体，就是1，然后所有的颜色在色度条中都体现在0和1之间。假如你需要512种颜色，则将1/512得到每两种颜色之间的步长。双重循环，按照步长为标准循环出每个颜色在色度条中的体现的值i，再次循环colors数组中的每一组，得到另一个数组j，（如j为0时，得到数组[ 0.0, '0x0000FF',colorval[0]]），将i与colors[ j ][ 0 ]以及colors[ j + 1 ][ 0 ]作比较，得到i所代表的颜色所在的区间。每个区间的变化标准不同，因此，我们按照区间分开处理。分别获取colors[ j ]以及colors[ j + 1 ]的值，分别获取它们的RGB值，简单运用一些数学等比的知识就可以得到每个i对应的值以及RGB（颜色），将得到的数据写入一个数组colorsArray。代码如下:

> for ( var i = 0; i <= 1; i += step ) {
>
> 　　for ( var j = 0; j < colors.length - 1; j ++ ) {
>
> 　　　　if ( i >= colors[ j ][ 0 ] && i < colors[ j + 1 ][ 0 ] ) {
>
> 　　　　　　var minv = colors[ j ][ 0 ], maxv = colors[ j + 1 ][ 0 ];
>
> 　　　　　　var minval = colors[ j ][ 2 ], maxval = colors[ j + 1 ][ 2 ];
>
> 　　　　　　var color = new THREE.Color( 0xffffff );
>
> 　　　　　　var minColor = new THREE.Color( 0xffffff ).setHex( colors[ j ][ 1 ] );
>
> 　　　　　　var maxColor = new THREE.Color( 0xffffff ).setHex( colors[ j + 1 ][ 1 ] );
>
> 　　　　　　var colormin = colors[ j ][ 1 ];
>
> 　　　　　　var colorminr = parseInt( colormin.charAt( 2 ) + colormin.charAt( 3 ), 16 );
>
> 　　　　　　var colorming = parseInt( colormin.charAt( 4 ) + colormin.charAt( 5 ), 16 );
>
> 　　　　　　var colorminb = parseInt( colormin.charAt( 6 ) + colormin.charAt( 7 ), 16 );
>
> 　　　　　　var colormax = colors[ j + 1 ][ 1 ];
>
> 　　　　　　var colormaxr = parseInt( colormax.charAt( 2 ) + colormax.charAt( 3 ), 16 );
>
> 　　　　　　var colormaxg = parseInt( colormax.charAt( 4 ) + colormax.charAt( 5 ), 16 );
>
> 　　　　　　var colormaxb = parseInt( colormax.charAt( 6 ) + colormax.charAt( 7 ), 16 );
>
> 　　　　　　var colorr = parseInt(((i - minv)/(maxv - minv))*(colormaxr - colorminr) + colorminr);
>
> 　　　　　　var colorg = parseInt(((i - minv)/(maxv - minv))*(colormaxg - colorming) + colorming);
>
> 　　　　　　var colorb = parseInt(((i - minv)/(maxv - minv))*(colormaxb - colorminb) + colorminb);
>
> 　　　　　　var color = colorr*256*256 + colorg*256 + colorb;
>
> 　　　　　　var colorvalue = (colorval[4] - colorval[0])*i + colorval[0];
>
> 　　　　　　var colorarr = [color,colorvalue];
>
> 　　　　　　colorsArray.push( colorarr );
>
> 　　　　}
>
> 　　}
>
> }

到这里我们得到了想要的colorsArray，里面包含了512组数据：颜色和颜色对应的值。下面我们只需要在添加物体的时候循环colorsArray数组，判断物体的值与colorsArray中那组数据的colorvalue相近，就选择相应的颜色为物体着色即可。修改d中的代码，这里以y轴值为例：

> var geometry = new THREE.SphereGeometry( 0.3, 32, 16 );
>
> var material = new THREE.MeshLambertMaterial( { color: 0x00ff00 } );
>
> for(m=0;m<1000;m++){
>
> 　　var sjs1=Math.random();
>
> 　　var sjs2=Math.random();
>
> 　　var sjs3=Math.random();
>
> 　　var meshpoint = 'mesh'+m;
>
> 　　for(n=0;n<colorsArray.length;n++){
>
> 　　　　if((Math.abs(160*sjs2 - colorsArray[n][1])) < 1){
>
> 　　　　　　var material = new THREE.MeshLambertMaterial( { color:colorsArray[n][0] } );
>
> 　　　　}
>
> 　　}
>
> 　　meshpoint = new THREE.Mesh( geometry, material );
>
> 　　meshpoint.position.set(160*sjs1,160*sjs2,160*sjs3);
>
> 　　this.mesh.add(meshpoint);
>
> }

**g.添加箭头**

坐标轴只有网格和坐标是可以区别物体坐标的，但是通常我们习惯带有箭头的坐标系，然而怎样才能加上箭头呢？

答案是用THREE.ArrowHelper。其中第一个参数是箭头起始点坐标，第二个参数是箭头终点坐标，第三个参数为箭头长度，最后为箭头颜色。用法示例：

> var originz = new THREE.Vector3(0,0,160);//箭头始点坐标
>
> var terminusz = new THREE.Vector3(0,0,180);//箭头终点坐标
>
> var directionz = new THREE.Vector3().subVectors(terminusz, originz).normalize();//箭头方向
>
> var arrowz = new THREE.ArrowHelper(directionz, originz, 30, 0xffffff);
>
> this.mesh.add(arrowz);//将箭头加入场景



#### 4.其它可能问题 

到了这里，three.js绘制三维坐标系的内容就结束了。内容比较多，上面的a、b、c、d不分顺序，这里主要介绍的是解决方法，看懂的小伙伴可以尝试一下。

另外，在实际绘图的时候可能会遇到**角度不对**或者**绘制图形偏大或者偏小**的问题。**角度不对**呢就调整相机的位置，相机的三个数值调整一下。图形偏大或者偏小也是调整相机的位置，**图形偏大**，相机三个坐标值调大一些；**图形偏小**的话，就将相机三个坐标调小一些。