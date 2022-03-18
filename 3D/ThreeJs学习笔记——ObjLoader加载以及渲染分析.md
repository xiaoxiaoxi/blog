# ThreeJs学习笔记——ObjLoader加载以及渲染分析

[![img](https://upload.jianshu.io/users/upload_avatars/5828513/598c359b-a5dd-47ea-a41b-a5d24f5239a9.jpg?imageMogr2/auto-orient/strip|imageView2/1/w/96/h/96/format/webp)](https://www.jianshu.com/u/7398ccc6f6e2)

[仰简](https://www.jianshu.com/u/7398ccc6f6e2)关注

0.3212018.12.11 11:25:14字数 2,159阅读 14,236

# 一、前言

这篇文章主要学习 ThreeJs 中的 demo [loader/obj2](https://threejs.org/examples/#webgl_loader_obj2)，主要是分析一下 obj 是如何加载的，纹理以及材质是如何加载的，3d camera 以及 camera controller 这些是如何实现的等。那么，先来 2 个 gif 图震撼一下吧。

![img]()

objloader2-拖动

![img]()

objloader2-放大.gif

# 二、代码分析

## 1.html 部分



```xml
<div id="glFullscreen">
    <!-- 渲染 3D 场景的 canvas -->
    <canvas id="example"></canvas>
</div>
<!-- dat gui 的 div 占位-->
<div id="dat">

</div>
<!--three.js 的其他一些信息说明-->
<div id="info">
    <a href="http://threejs.org" target="_blank" rel="noopener">three.js</a> - OBJLoader2 direct loader test
    <div id="feedback"></div>
</div>
```

这一部分最重要的就是这个 <canvas></canvas> 标记的添加，也说明了 WebGL 的主要实现就去用这个 canvas 去绘制。这和 Android 端上的原生 API 很像嘛。

## 2.script 导入



```xml
<!-- 导入 threejs 核心库 -->
<script src="../build/three.js"></script>
<!-- 导入 camera controller，用于响应鼠标/手指的拖动，放大，旋转等操作 -->
<script src="js/controls/TrackballControls.js"></script>
<!-- 材质加载 -->
<script src="js/loaders/MTLLoader.js"></script>
<!-- 三方库 dat gui 库的导入-->
<script src="js/libs/dat.gui.min.js"></script>
<!-- 三方库 stats 的导入-->
<script type="text/javascript" src="js/libs/stats.min.js"></script>
<!-- 构建 mesh,texture 等支持 -->
<script src="js/loaders/LoaderSupport.js"></script>
<!-- 加载 obj 的主要实现 -->
<script src="js/loaders/OBJLoader2.js"></script>
```

## 3.模型加载

![img](https://upload-images.jianshu.io/upload_images/5828513-5080a473e13e1bfc.jpg?imageMogr2/auto-orient/strip|imageView2/2/w/1200/format/webp)

objloader2时序图.jpg

### 3.1 定义OBJLoader2Example

在[ThreeJS 学习笔记——JavaScript 中的函数与对象](https://www.jianshu.com/p/c526f6934736)中了解到，JavaScript 中是通过原型(prototype)来实现面向对象编程。这里先定义了函数 OBJLoader2Example()，然后再指定OBJLoader2Example的 prototype 的 constructor 为 OBJLoader2Example() 本身，这也就定义了一个 “类” OBJLoader2Example，我们可以使用这个类来声明新的对象。



```jsx
var OBJLoader2Example = function ( elementToBindTo ) {......};
OBJLoader2Example.prototype = {
    constructor: OBJLoader2Example,
        initGL: function () {......},
        initContent: function () {......},
        _reportProgress: function () {......},
        resizeDisplayGL: function () {......},
        recalcAspectRatio: function () {......},
        resetCamera: function () {......},
        updateCamera: function () {......},
        render: function () {......}
}
```

### 3.2 OBJLoader2Example 的构造方法



```kotlin
var OBJLoader2Example = function ( elementToBindTo ) {
                // 渲染器，后面它会绑定 canvas 节点
                this.renderer = null;
                // canvas 节点
                this.canvas = elementToBindTo;
                // 视图比例
                this.aspectRatio = 1;
                this.recalcAspectRatio();
                // 3D 场景
                this.scene = null;
                // 默认相机参数
                this.cameraDefaults = {
                    // 相机的位置，就是相机该摆在哪里
                    posCamera: new THREE.Vector3( 0.0, 175.0, 500.0 ),
                    // 相机的目标
                    posCameraTarget: new THREE.Vector3( 0, 0, 0 ),
                    // 近截面
                    near: 0.1,
                    // 远截面
                    far: 10000,
                    // 视景体夹角
                    fov: 45
                };
                // 3D 相机
                this.camera = null;
                // 3D 相机的目标，就是相机该盯着哪里看
                this.cameraTarget = this.cameraDefaults.posCameraTarget;
                // 3D 相机控制器，当然也可理解就是一个手势控制器
                this.controls = null;
            };
```

构造方法主要是属性的定义，代码中添加了注释简要介绍了各个属性的作用，总体来说就是3D场景，3D 相机，相机控制器以及最重要的渲染器，渲染器绑定了 canvas，3D 场景及其所有的物件都会通过这个渲染器渲染到 canvas 中去。

### 3.3 initGL()



```kotlin
initGL: function () {
                    // 创建渲染器
                    this.renderer = new THREE.WebGLRenderer( {
                        // 绑定 canvas
                        canvas: this.canvas,
                        // 抗锯齿
                        antialias: true,
                        autoClear: true
                    } );
                    this.renderer.setClearColor( 0x050505 );

                    this.scene = new THREE.Scene();
                    // 初始化透视投影相机，这是一个三角的景锥体，物体在其里面呈现的效果是近大远小
                    this.camera = new THREE.PerspectiveCamera( this.cameraDefaults.fov, this.aspectRatio, this.cameraDefaults.near, this.cameraDefaults.far );
                    this.resetCamera();
                    // 初始化 controller
                    this.controls = new THREE.TrackballControls( this.camera, this.renderer.domElement );

                    // 添加环境光与平行光
                    var ambientLight = new THREE.AmbientLight( 0x404040 );
                    var directionalLight1 = new THREE.DirectionalLight( 0xC0C090 );
                    var directionalLight2 = new THREE.DirectionalLight( 0xC0C090 );

                    directionalLight1.position.set( -100, -50, 100 );
                    directionalLight2.position.set( 100, 50, -100 );

                    this.scene.add( directionalLight1 );
                    this.scene.add( directionalLight2 );
                    this.scene.add( ambientLight );
                    // 添加调试网格
                    var helper = new THREE.GridHelper( 1200, 60, 0xFF4444, 0x404040 );
                    this.scene.add( helper );
                },
```

initGL() 方法中初始化了各个属性，同时还添加了环境光与平行光源，以用于调试的网格帮助模型。在 3D 场景中很多物体都可看成是一个模型，如这里的光源。而 camera 在有一些渲染框架中也会被认为是一个模型，但其只是一个用于参与 3D 渲染时的参数。camera 最主要的作用是决定了投影矩阵，在投影矩阵内的物体可见，而不在里面则不可见。

### 4. initContent()



```jsx
initContent: function () {
                    var modelName = 'female02';
                    this._reportProgress( { detail: { text: 'Loading: ' + modelName } } );

                    var scope = this;
                    // 声明 ObjLoader2 对象
                    var objLoader = new THREE.OBJLoader2();
                    // 模型加载完成的 call back，加载完成后便会把模型加载到场景中
                    var callbackOnLoad = function ( event ) {
                        scope.scene.add( event.detail.loaderRootNode );
                        console.log( 'Loading complete: ' + event.detail.modelName );
                        scope._reportProgress( { detail: { text: '' } } );
                    };
                    // 材质加载完成的回调，材质加载完成后便会进一步加 obj
                    var onLoadMtl = function ( materials ) {
                        objLoader.setModelName( modelName );
                        objLoader.setMaterials( materials );
                        objLoader.setLogging( true, true );
                        // 开始加载 obj
                        objLoader.load( 'models/obj/female02/female02.obj', callbackOnLoad, null, null, null, false );
                    };
                    // 开始加载材质
                    objLoader.loadMtl( 'models/obj/female02/female02.mtl', null, onLoadMtl );
                },
```

内容加载这一块是重点，其主要是通过 ObjLoader2 先是加载了材质然后加载模型。关于 obj 和 mtl 文件， 请打开 female02.obj 和 female02.mtl，可以发现它就是一个文本文件，通过注释来感受一下其文件格式如何。

**female02.obj部分数据**



```bash
# Blender v2.54 (sub 0) OBJ File: ''
# www.blender.org
# obj对应的材质文件
mtllib female02.mtl
# o 对象名称(Object name)
o mesh1.002_mesh1-geometry
# 顶点
v 15.257854 104.640892 8.680023
v 14.044281 104.444138 11.718708
v 15.763498 98.955704 11.529579
......
# 纹理坐标
vt 0.389887 0.679023
vt 0.361250 0.679023
vt 0.361250 0.643346
......
# 顶点法线
vn 0.945372 0.300211 0.126926
vn 0.794275 0.212683 0.569079
vn 0.792047 0.184729 0.581805
......
# group
g mesh1.002_mesh1-geometry__03_-_Default1noCulli__03_-_Default1noCulli
# 当前图元所用材质
usemtl _03_-_Default1noCulli__03_-_Default1noCulli
s off
# v1/vt1/vn1 v2/vt2/vn2 v3/vt3/vn3(索引起始于1)    
f 1/1/1 2/2/2 3/3/3
f 1/1/1 4/4/4 2/2/2
f 4/4/4 1/1/1 5/5/5
......
```

**female02.mtl部分数据**



```css
......
# 定义一个名为 _03_-_Default1noCulli__03_-_Default1noCulli 的材质
newmtl _03_-_Default1noCulli__03_-_Default1noCulli
# 反射指数 定义了反射高光度。该值越高则高光越密集，一般取值范围在0~1000。
Ns 154.901961
# 材质的环境光（ambient color）
Ka 0.000000 0.000000 0.000000
# 散射光（diffuse color）用Kd
Kd 0.640000 0.640000 0.640000
# 镜面光（specular color）用Ks
Ks 0.165000 0.165000 0.165000
# 折射值 可在0.001到10之间进行取值。若取值为1.0，光在通过物体的时候不发生弯曲。玻璃的折射率为1.5。
Ni 1.000000
# 渐隐指数描述 参数factor表示物体融入背景的数量，取值范围为0.0~1.0，取值为1.0表示完全不透明，取值为0.0时表示完全透明。
d 1.000000
# 指定材质的光照模型。illum后面可接0~10范围内的数字参数。各个参数代表不同的光照模型
illum 2
# 为漫反射指定颜色纹理文件
map_Kd 03_-_Default1noCulling.JPG
......
```

关于 obj 和 mtl 文件中各个字段的意思都在注释中有说明了，至于每个字段参数如何使用，就需要对 OpenGL 如何渲染模型有一定的了解了。继续来看材质的加载和obj 的加载。

#### 4.1 ObjectLoader2#loadMtl()



```jsx
loadMtl: function ( url, content, onLoad, onProgress, onError, crossOrigin, materialOptions ) {
        ......
        this._loadMtl( resource, onLoad, onProgress, onError, crossOrigin, materialOptions );
},
```

调用了内部的_loadMtl()，_loadMtl() 函数的实现代码是有点多的，不过不要紧，我给做了精简。



```jsx
_loadMtl: function ( resource, onLoad, onProgress, onError, crossOrigin, materialOptions ) {
    ......
    // 7. 创建了 materialCreator 后，就会加载到这里。这里最后通过 onLoad 通知给调用者，调用者继续加载模型。
    var processMaterials = function ( materialCreator ) {
        ......
        // 8.创建材质
        materialCreator.preload();
       // 9.回调给调用者
        onLoad( materials, materialCreator );
    }
    ......
    // 1. 构建一个 MTLLoader
    var mtlLoader = new THREE.MTLLoader( this.manager );
   // 4.文件加载成功后回调到 parseTextWithMtlLoader 这里
    var parseTextWithMtlLoader = function ( content ) {
        ......
        contentAsText = THREE.LoaderUtils.decodeText( content );
        ......
        // 5.对文件内容进行解析，解析完成后得到一个 materialCreator 对象，然后再调用 processMaterials
        processMaterials( mtlLoader.parse( contentAsText ) );
    }
    ......
    // 2.构建一个 FileLoader
    var fileLoader = new THREE.FileLoader( this.manager );
    ......
   // 3. 加载文件，文件加载成功能后回调 parseTextWithMtlLoader
    fileLoader.load( resource.url, parseTextWithMtlLoader, onProgress, onError );
}
```

注释里包含了材质加载的整个逻辑，一共 9 个步骤，但这里重点只需要关注以下 3 个步骤：

**(1)文件加载——FileLoader#load()**



```php
load: function ( url, onLoad, onProgress, onError ) {
    ......
    var request = new XMLHttpRequest();
    request.open( 'GET', url, true );
    ......
}
```

FileLoader 是 ThreeJs 库中的代码，关于 load() 方法中的前后代码这里都略去了，重点是知道了它是通过 Get 请求来获取的。

**(2)文件parse——MTLLoader#parse()**



```csharp
parse: function ( text, path ) {

        var lines = text.split( '\n' );
        var info = {};
        var delimiter_pattern = /\s+/;
        var materialsInfo = {};

        for ( var i = 0; i < lines.length; i ++ ) {

            var line = lines[ i ];
            line = line.trim();

            if ( line.length === 0 || line.charAt( 0 ) === '#' ) {

                // Blank line or comment ignore
                continue;

            }

            var pos = line.indexOf( ' ' );

            var key = ( pos >= 0 ) ? line.substring( 0, pos ) : line;
            key = key.toLowerCase();

            var value = ( pos >= 0 ) ? line.substring( pos + 1 ) : '';
            value = value.trim();

            if ( key === 'newmtl' ) {

                // New material

                info = { name: value };
                materialsInfo[ value ] = info;

            } else {

                if ( key === 'ka' || key === 'kd' || key === 'ks' ) {

                    var ss = value.split( delimiter_pattern, 3 );
                    info[ key ] = [ parseFloat( ss[ 0 ] ), parseFloat( ss[ 1 ] ), parseFloat( ss[ 2 ] ) ];

                } else {

                    info[ key ] = value;

                }

            }

        }

        var materialCreator = new THREE.MTLLoader.MaterialCreator( this.resourcePath || path, this.materialOptions );
        materialCreator.setCrossOrigin( this.crossOrigin );
        materialCreator.setManager( this.manager );
        materialCreator.setMaterials( materialsInfo );
        return materialCreator;

    }
```

parse() 方法的代码看起来有点多，但其实很简单，就是对着 mtl 文件一行一行的解析。这里的重点是创建了 MaterialCreator并且保存在了 materialsInfo 中。materialsInfo 是一个 map 对象，其中保存的值最重要的是包括了 map_Kd，这个在创建材质时要加载的纹理。

**(3)创建材质——MaterialCreator#preload()**



```jsx
preload: function () {
        for ( var mn in this.materialsInfo ) {
            this.create( mn );
        }
    },
```

preload() 中就遍历每一个 material 然后分别调用 create() 。而 create() 又是进一步调用了 createMaterial_() 方法。



```csharp
createMaterial_: function ( materialName ) {
        // Create material
        var scope = this;
        var mat = this.materialsInfo[ materialName ];
        var params = {
            name: materialName,
            side: this.side
        };
        function resolveURL( baseUrl, url ) {
            if ( typeof url !== 'string' || url === '' )
                return '';
            // Absolute URL
            if ( /^https?:\/\//i.test( url ) ) return url;
            return baseUrl + url;
        }
        function setMapForType( mapType, value ) {
            if ( params[ mapType ] ) return; // Keep the first encountered texture
            var texParams = scope.getTextureParams( value, params );
            var map = scope.loadTexture( resolveURL( scope.baseUrl, texParams.url ) );
            map.repeat.copy( texParams.scale );
            map.offset.copy( texParams.offset );
            map.wrapS = scope.wrap;
            map.wrapT = scope.wrap;
            params[ mapType ] = map;
        }
        for ( var prop in mat ) {
            var value = mat[ prop ];
            var n;
            if ( value === '' ) continue;
            switch ( prop.toLowerCase() ) {
                // Ns is material specular exponent
                case 'kd':
                    // Diffuse color (color under white light) using RGB values
                    params.color = new THREE.Color().fromArray( value );
                    break;
                case 'ks':
                    // Specular color (color when light is reflected from shiny surface) using RGB values
                    params.specular = new THREE.Color().fromArray( value );
                    break;
                case 'map_kd':
                    // Diffuse texture map
                    setMapForType( "map", value );
                    break;
                case 'map_ks':
                    // Specular map
                    setMapForType( "specularMap", value );
                    break;
                case 'norm':
                    setMapForType( "normalMap", value );
                    break;
                case 'map_bump':
                case 'bump':
                    // Bump texture map
                    setMapForType( "bumpMap", value );
                    break;
                case 'map_d':
                    // Alpha map
                    setMapForType( "alphaMap", value );
                    params.transparent = true;
                    break;
                case 'ns':
                    // The specular exponent (defines the focus of the specular highlight)
                    // A high exponent results in a tight, concentrated highlight. Ns values normally range from 0 to 1000.
                    params.shininess = parseFloat( value );
                    break;
                case 'd':
                    n = parseFloat( value );
                    if ( n < 1 ) {
                        params.opacity = n;
                        params.transparent = true;
                    }
                    break;
                case 'tr':
                    n = parseFloat( value );
                    if ( this.options && this.options.invertTrProperty ) n = 1 - n;
                    if ( n > 0 ) {
                        params.opacity = 1 - n;
                        params.transparent = true;
                    }
                    break;
                default:
                    break;
            }
        }
        this.materials[ materialName ] = new THREE.MeshPhongMaterial( params );
        return this.materials[ materialName ];
    },
```

这里就是告知我们该怎么用 mtl 文件中的每个字段了，这里主要关注一下纹理图片是如何加载的，其他的字段参数再看看 mtl 的注释就可以理解了。map-kd、map_ks、norm、map_bump、bump 以及 map_d 的处理是调用了setMapForType()，他们都是去加载纹理的，只是纹理的形式不一样。



```php
function setMapForType( mapType, value ) {
            ......
            var map = scope.loadTexture( resolveURL( scope.baseUrl, texParams.url ) );
            ......
}
```

这里的 loadTexture() 就是加载纹理的实现，一般来说在材质文件中对纹理的地址要写成相对的，这里会根据材质的地址的 base url 来 resolve 出一个纹理的地址。继续来看loadTexture()。



```php
loadTexture: function ( url, mapping, onLoad, onProgress, onError ) {
    ......
    var loader = THREE.Loader.Handlers.get( url );
    ......
    loader = new THREE.TextureLoader( manager );
   ......
    texture = loader.load( url, onLoad, onProgress, onError );
    return texture;
}
```

其主要是构建一个 TextureLoader，然后调用其 load() 进行加载。



```jsx
load: function ( url, onLoad, onProgress, onError ) {
  ......
  var loader = new ImageLoader( this.manager );
  ......
  loader.load( url, function ( image ) {}
}
```

又进一步通过了 ImageLoader 来加载。



```jsx
load: function ( url, onLoad, onProgress, onError ) {
  ......
  var image = document.createElementNS( 'http://www.w3.org/1999/xhtml', 'img' );
......
image.src = url;
return image;
}
```

原来图片的加载是通过创建一个 <img> 标记来加载的。创建一个 <img> 标记，在不添加到 dom 树中的情况下，只要给 src 赋了值，就会去下载图片了。

到这里，终于把材质以及纹理的加载分析完了。接下来继续分析 obj 的加载。

#### 4.2ObjLoader2#load()



```jsx
    load: function ( url, onLoad, onProgress, onError, onMeshAlter, useAsync ) {
        var resource = new THREE.LoaderSupport.ResourceDescriptor( url, 'OBJ' );
        this._loadObj( resource, onLoad, onProgress, onError, onMeshAlter, useAsync );
    },
```

同样是进一步的调用，这里调用的是 _loadObj()。



```jsx
_loadObj: function ( resource, onLoad, onProgress, onError, onMeshAlter, useAsync ) {
    ......
    var fileLoaderOnLoad = function ( content ) {
       ......
       ......
       // 3.解析 obj
       loaderRootNode: scope.parse( content ),
       ......
    },
    // 1.构建 FileLoader
    var fileLoader = new THREE.FileLoader( this.manager );
    ......
    // 2.加载文件，这里在加载 mtl 的时候已经分析过了，并且最后会回调到 fileLoaderOnLoad
    fileLoader.load( resource.name, fileLoaderOnLoad, onProgress, onError );
}
```

_loadObj() 的代码这里也精简了一下，并在注释中说明了逻辑。文件加载已经在前面分析过了，这里就关注一下解析 obj。



```php
/**
* Parses OBJ data synchronously from arraybuffer or string.
*
* @param {arraybuffer|string} content OBJ data as Uint8Array or String
*/
parse: function ( content ) {
    ......
    // 1.初始化 meshBuilder
    this.meshBuilder.init(); 
    // 2.创建一个 Parser
    var parser = new THREE.OBJLoader2.Parser();
    ......
    var onMeshLoaded = function ( payload ) {
        // 4.从 meshBuilder 中获取 mesh ，并把 mesh 都加到节点中
        var meshes = scope.meshBuilder.processPayload( payload );
        var mesh;
        for ( var i in meshes ) {
            mesh = meshes[ i ];
            scope.loaderRootNode.add( mesh );
        }
    } 
   ......
   // 3.解析文本，因为这里传输的就是文本
   parser.parseText( content );
   ......
}
```

这里的重点是parseText()。



```jsx
parseText: function ( text ) {
    ......
    for ( var char, word = '', bufferPointer = 0, slashesCount = 0, i = 0; i < length; i++ ) {
          ......
          this.processLine( buffer, bufferPointer, slashesCount );
          ......
    }
    ......
}
```

同样，省略的部分这里可以先不看，来看一看具体解析 obj 文件的 processLine()。



```kotlin
     processLine: function ( buffer, bufferPointer, slashesCount ) {
        if ( bufferPointer < 1 ) return;

        var reconstructString = function ( content, legacyMode, start, stop ) {
            var line = '';
            if ( stop > start ) {

                var i;
                if ( legacyMode ) {

                    for ( i = start; i < stop; i++ ) line += content[ i ];

                } else {


                    for ( i = start; i < stop; i++ ) line += String.fromCharCode( content[ i ] );

                }
                line = line.trim();

            }
            return line;
        };

        var bufferLength, length, i, lineDesignation;
        lineDesignation = buffer [ 0 ];
        switch ( lineDesignation ) {
            case 'v':
                this.vertices.push( parseFloat( buffer[ 1 ] ) );
                this.vertices.push( parseFloat( buffer[ 2 ] ) );
                this.vertices.push( parseFloat( buffer[ 3 ] ) );
                if ( bufferPointer > 4 ) {

                    this.colors.push( parseFloat( buffer[ 4 ] ) );
                    this.colors.push( parseFloat( buffer[ 5 ] ) );
                    this.colors.push( parseFloat( buffer[ 6 ] ) );

                }
                break;

            case 'vt':
                this.uvs.push( parseFloat( buffer[ 1 ] ) );
                this.uvs.push( parseFloat( buffer[ 2 ] ) );
                break;

            case 'vn':
                this.normals.push( parseFloat( buffer[ 1 ] ) );
                this.normals.push( parseFloat( buffer[ 2 ] ) );
                this.normals.push( parseFloat( buffer[ 3 ] ) );
                break;

            case 'f':
                bufferLength = bufferPointer - 1;

                // "f vertex ..."
                if ( slashesCount === 0 ) {

                    this.checkFaceType( 0 );
                    for ( i = 2, length = bufferLength; i < length; i ++ ) {

                        this.buildFace( buffer[ 1 ] );
                        this.buildFace( buffer[ i ] );
                        this.buildFace( buffer[ i + 1 ] );

                    }

                    // "f vertex/uv ..."
                } else if  ( bufferLength === slashesCount * 2 ) {

                    this.checkFaceType( 1 );
                    for ( i = 3, length = bufferLength - 2; i < length; i += 2 ) {

                        this.buildFace( buffer[ 1 ], buffer[ 2 ] );
                        this.buildFace( buffer[ i ], buffer[ i + 1 ] );
                        this.buildFace( buffer[ i + 2 ], buffer[ i + 3 ] );

                    }

                    // "f vertex/uv/normal ..."
                } else if  ( bufferLength * 2 === slashesCount * 3 ) {

                    this.checkFaceType( 2 );
                    for ( i = 4, length = bufferLength - 3; i < length; i += 3 ) {

                        this.buildFace( buffer[ 1 ], buffer[ 2 ], buffer[ 3 ] );
                        this.buildFace( buffer[ i ], buffer[ i + 1 ], buffer[ i + 2 ] );
                        this.buildFace( buffer[ i + 3 ], buffer[ i + 4 ], buffer[ i + 5 ] );

                    }

                    // "f vertex//normal ..."
                } else {

                    this.checkFaceType( 3 );
                    for ( i = 3, length = bufferLength - 2; i < length; i += 2 ) {

                        this.buildFace( buffer[ 1 ], undefined, buffer[ 2 ] );
                        this.buildFace( buffer[ i ], undefined, buffer[ i + 1 ] );
                        this.buildFace( buffer[ i + 2 ], undefined, buffer[ i + 3 ] );

                    }

                }
                break;

            case 'l':
            case 'p':
                bufferLength = bufferPointer - 1;
                if ( bufferLength === slashesCount * 2 )  {

                    this.checkFaceType( 4 );
                    for ( i = 1, length = bufferLength + 1; i < length; i += 2 ) this.buildFace( buffer[ i ], buffer[ i + 1 ] );

                } else {

                    this.checkFaceType( ( lineDesignation === 'l' ) ? 5 : 6  );
                    for ( i = 1, length = bufferLength + 1; i < length; i ++ ) this.buildFace( buffer[ i ] );

                }
                break;

            case 's':
                this.pushSmoothingGroup( buffer[ 1 ] );
                break;

            case 'g':
                // 'g' leads to creation of mesh if valid data (faces declaration was done before), otherwise only groupName gets set
                this.processCompletedMesh();
                this.rawMesh.groupName = reconstructString( this.contentRef, this.legacyMode, this.globalCounts.lineByte + 2, this.globalCounts.currentByte );
                break;

            case 'o':
                // 'o' is meta-information and usually does not result in creation of new meshes, but can be enforced with "useOAsMesh"
                if ( this.useOAsMesh ) this.processCompletedMesh();
                this.rawMesh.objectName = reconstructString( this.contentRef, this.legacyMode, this.globalCounts.lineByte + 2, this.globalCounts.currentByte );
                break;

            case 'mtllib':
                this.rawMesh.mtllibName = reconstructString( this.contentRef, this.legacyMode, this.globalCounts.lineByte + 7, this.globalCounts.currentByte );
                break;

            case 'usemtl':
                var mtlName = reconstructString( this.contentRef, this.legacyMode, this.globalCounts.lineByte + 7, this.globalCounts.currentByte );
                if ( mtlName !== '' && this.rawMesh.activeMtlName !== mtlName ) {

                    this.rawMesh.activeMtlName = mtlName;
                    this.rawMesh.counts.mtlCount++;
                    this.checkSubGroup();

                }
                break;

            default:
                break;
        }
    },
```

这段代码就比较长了，有 150 多行，但内容其实很简单，就是根据 obj 的文件格式进行解析。如果看到这里忘记了 obj 的文件格式，那建议先回顾一下。解析的过程已经非常细节了，就不详细展开了。这里最后的解析结果就是顶点，纹理坐标以及法向根据 face 的索引进行展开，得到的结果是 **vvv | vtvt | vnvnvn** 这样的 n 组顶点数组 以及 n 组索引数组。顶点数组，索引数组以及材质/纹理构成了用于渲染的3D网格 mesh。

到这里 obj 的加载也分析完了。obj 的加载是主体，但也是最简单的。容易出问题的是在材质和纹理的加载上，需要注意的问题比较多。

### 5.render()



```jsx
var render = function () {
    requestAnimationFrame( render );
    app.render();
};
```

这个 render 是一个函数，不是OBJLoader2Example 的方法，是在 <script></script> 里面的。其首先请求了动画刷新回调，使得其可以监听到浏览器的刷新。刷新时把回调函数设为自己，使得浏览器在不断刷新的过程中调用 render() 函数。然后才是调用 OBJLoader2Example 的 render() 方法进行 3D 场景的绘制。这里简单的看一下 MDN 对 requestAnimationFrame 的描述。

> window.requestAnimationFrame() 方法告诉浏览器您希望执行动画并请求浏览器在下一次重绘之前调用指定的函数来更新动画。该方法使用一个回调函数作为参数，这个回调函数会在浏览器重绘之前调用。
> 当你需要更新屏幕画面时就可以调用此方法。在浏览器下次重绘前执行回调函数。**回调的次数通常是每秒60次**，但大多数浏览器通常匹配 W3C 所建议的刷新频率。

看到加粗的字体了吗，这和端的刷新频率是一样的，即 60 fps。然后再来简单分析下 OBJLoader2Example 的 render() 方法。



```kotlin
render: function () {
    if ( ! this.renderer.autoClear ) this.renderer.clear();
    this.controls.update();
    this.renderer.render( this.scene, this.camera );
}
```

可以看到这里主要就是通过 WebGLRenderer 进行实际的渲染，那这里再进一步分析就到 OpenGL 了。关于 OpenGL 是一个比较大的课题，就不在这里分析了，也不合适。

# 三、后记

文章主要分析了 ThreeJs 是如何加载一个 Obj 模型并将其渲染出来的过程，分析的过程很长，但实际并不复杂，并不涉及到什么难理解的概念。分析前由于 JavaScript 的水平实在有限，所以还特定去补了一刀[《ThreeJS 学习笔记——JavaScript 中的函数与对象》](https://www.jianshu.com/p/c526f6934736)。在比较深入的理解了函数与对象之后，再加上基本的 OpenGL 基础，一步一步的分析这个加载的过程其实还是比较轻松的。

最后，感谢你能读到并读完此文章。希望我简陋的分析以及分享对你有所帮助，同时也请帮忙点个赞，鼓励我继续分析。