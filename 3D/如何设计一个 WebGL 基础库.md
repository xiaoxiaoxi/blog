# 如何设计一个 WebGL 基础库

[![img](https://p3-passport.byteacctimg.com/img/user-avatar/ecbaedae9c3d45716d5c30f94436877b~300x300.image)](https://juejin.cn/user/1626932938285976)

[doodlewind ![lv-6](https://lf3-cdn-tos.bytescm.com/obj/static/xitu_juejin_web/74bd93adef7feff4fee26d08c0845b4f.svg)](https://juejin.cn/user/1626932938285976)

2019年11月25日 09:08 · 阅读 5204

关注

![如何设计一个 WebGL 基础库](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea170651f018a6~tplv-t2oaga2asx-zoom-crop-mark:1304:1304:1304:734.awebp)

要想使用 WebGL 直通 GPU 的渲染能力，很多同学的第一反应就是使用现成的开源项目，如著名的 Three.js 等。但是，直接套用它们就是唯一的选择了吗？如果想深入 WebGL 基础甚至自己造轮子，又该从何下手呢？本文希望以笔者自己的实践经验为例，科普一些图形基础库设计层面的知识。

## 背景

不久前，我们为 [稿定设计 Web 端](https://link.juejin.cn/?target=https%3A%2F%2Fgaoding.com) 添加了 3D 文字的编辑能力。你可以将原本局限在二维平面上的文字立体化，为其添加丰富的质感，就像这样：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016cb4757bf8~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



3D 文字的 WebGL 渲染部分，使用了我们自研的 [Beam](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam) 基础库。它并不是某个开源项目的 fork 魔改版，而是从头开始正向实现的。作为 Beam 的作者，推动一个新轮子在生产环境中落地的经历，无疑给了我很多值得分享的经验。下面就先从最基本的定位出发，聊聊 WebGL 基础库吧。

## 渲染引擎与 WebGL 基础库

提到 WebGL 时，大家普遍会想到 Three.js 这样的开源项目，这多少有点「用 React 全家桶代表 Web 前端」 的感觉。其实，Three 已经是个颇为高层的 3D 渲染引擎了。它和 Beam 这样的 WebGL 基础库之间，粗略来说有这些异同：

- 渲染引擎需要屏蔽 WebGL 等渲染端的内部概念，基础库则要开放这些概念。
- 渲染引擎还可以有 SVG / Canvas 等多个渲染端，基础库则专注一个渲染端。
- 渲染引擎的设计是针对 3D 或 2D 等特定场景的，基础库则没有这种假设。
- 渲染引擎在体积上通常更重，基础库则显然较轻。

其实，我更愿意把 Three 和 Beam 的对比，当做 React 和 jQuery 的对比：**一个想将渲染端的复杂度屏蔽到极致，另一个则想将直接操作渲染端的 API 简化到极致**。有鉴于图形渲染管线的高度灵活性，再加上重量级上的显著区别（Three 源码体积已超过 1M，且 Tree Shaking 效果不佳），笔者相信凡是希望追求控制的场景，都可以是 WebGL 基础库的用武之地。

> 社区有 Regl 这样流行的 WebGL 基础库，这证明类似的轮子并不是个伪需求。

## WebGL 概念抽象

在设计基础库的实际 API 前，我们至少需要清楚 WebGL 是如何工作的。WebGL 代码有很多琐碎之处，一头扎进代码里，容易使我们只见树木不见森林。根据笔者的理解，整个 WebGL 应用中我们操作的概念，其实不外乎这几个：

- **Shader** 着色器，是**存放图形算法的对象**。 相比于在 CPU 上单线程执行的 JS 代码，着色器在 GPU 上并行执行，计算出每帧数百万个像素各自的颜色。
- **Resource** 资源，是**存放图形数据的对象**。就像 JSON 成为 Web App 的数据那样，资源是传递给着色器的数据，包括大段的顶点数组、纹理图像，以及全局的配置项等。
- **Draw** 绘制，是**选好资源后运行着色器的请求**。要想渲染真实际的场景，一般需要多组着色器与多个资源，来回绘制多次才能完成一帧。每次绘制前，我们都需要选好着色器，并为其关联好不同的资源，也都会启动一次图形渲染管线。
- **Command** 命令，是**执行绘制前的配置**。WebGL 是非常有状态的。每次绘制前，我们都必须小心地处理好状态机。这些状态变更就是通过命令来实现的。Beam 基于一些约定大幅简化了人工的命令管理，当然你也可以定制自己的命令。

这些概念是如何协同工作的呢？请看下图：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016cb3f1de88~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



图中的 Buffers / Textures / Uniforms 都属于典型的资源。一帧当中可能存在多次绘制，每次绘制都需要着色器和相应的资源。在绘制之间，我们通过命令来管理好 WebGL 的状态。这就是笔者在设计 Beam 时，为 WebGL 建立的思维模型了。

理解这个思维模型很重要。因为 Beam 的 API 设计就是完全依据这个模型而实现的。让我们进一步看看一个实际的场景吧：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016cb41d8cd2~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



图中我们绘制了很多质感不同的球体。这一帧的渲染，则可以这样解构到上面的这些概念下：

- **着色器**无疑就是球体质感的渲染算法。对经典的 3D 游戏来说，要渲染不同质感的物体，经常需要切换不同的着色器。但现在基于物理的渲染算法流行后，这些球体也不难做到使用同一个着色器来渲染。
- **资源**包括了大段的球体顶点数据、材质纹理的图像数据，以及光照参数、变换矩阵等配置项。
- **绘制**是分多次进行的。我们选择每次绘制一个球体，而每次绘制也都会启动一次图形渲染管线。
- **命令**则是相邻的球体绘制之间，所执行的那些状态变更。

如何理解状态变更呢？不妨将 WebGL 想象成一个具备大量开关与接口的仪器。每次按下启动键（执行绘制）前。你都要配置好一堆开关，再连接好一条接着色器的线，和一堆接资源的线，就像这样：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016cc716ede3~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



还有很重要的一点，那就是虽然我们已经知道，一帧画面可以通过多次绘制而生成，而每次绘制又对应执行一次图形渲染管线的执行。但是，所谓的图形渲染管线又是什么呢？这对应于这张图：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016cc0c7e8b3~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



渲染管线，一般指的就是这样一个 GPU 上由顶点数据到像素的过程。现代的可编程 GPU 来说，管线中的某些阶段是可编程的。WebGL 标准里，这对应于图中蓝色的顶点着色器和片元着色器阶段。你可以把它们想象成两个需要你来写的函数。它们大体上分别做这样的工作：

- 顶点着色器输入原始的顶点坐标，输出根据你的需求变换后的坐标。
- 片元着色器输入一个像素位置，输出根据你的需求计算出的像素颜色。

以上这些就是笔者从基础库设计者的视角出发，所看到的 WebGL 基础概念啦。

## API 基础设计

虽然上面的章节完全没有涉及代码，但充分理清楚概念后，编码就是水到渠成的了。由于命令可以被自动化，在设计 Beam 时，笔者只定义了三个核心 API，分别是

- **beam.shader**
- **beam.resource**
- **beam.draw**

它们各自对应于管理着色器、资源和绘制。让我们看看怎样基于这个设计，来绘制 WebGL 中的 Hello World 三角形吧：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016debbde9c8~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



Beam 的代码示例如下：

```
import { Beam, ResourceTypes } from 'beam-gl'
import { MyShader } from './my-shader.js'
const { VertexBuffers, IndexBuffer } = ResourceTypes

const canvas = document.querySelector('canvas')
const beam = new Beam(canvas)

const shader = beam.shader(MyShader)
const vertexBuffers = beam.resource(VertexBuffers, {
  position: [
    -1, -1, 0, // vertex 0, bottom left
    0, 1, 0, // vertex 1, top middle
    1, -1, 0 // vertex 2, bottom right
  ],
  color: [
    1, 0, 0, // vertex 0, red
    0, 1, 0, // vertex 1, green
    0, 0, 1 // vertex 2, blue
  ]
})
const indexBuffer = beam.resource(IndexBuffer, {
  array: [0, 1, 2]
})

beam
  .clear()
  .draw(shader, vertexBuffers, indexBuffer)
复制代码
```

下面逐个介绍一些重要的 API 片段。首先自然是用 Canvas 初始化出 Beam 了：

```
const canvas = document.querySelector('canvas')
const beam = new Beam(canvas)
复制代码
```

然后我们用 `beam.shader` 来实例化着色器，这里的 `MyShader` 稍后再说：

```
const shader = beam.shader(MyShader)
复制代码
```

着色器准备好之后，就是准备资源了。为此我们需要使用 `beam.resource` API 来创建三角形的数据。这些数据装在不同的 Buffer 里，而 Beam 使用 `VertexBuffers` 类型来表达它们。三角形有 3 个顶点，每个顶点有两个属性 (attribute)，即 **position** 和 **color**，每个属性都对应于一个独立的 Buffer。这样我们就不难用普通的 JS 数组（或 TypedArray）来声明这些顶点数据了。Beam 会替你将它们上传到 GPU：

> 注意区分 WebGL 中的**顶点**和**坐标**概念。顶点 (vertex) 不仅可以包含一个点的坐标属性，还可以包含法向量、颜色等其它属性。这些属性都可以输入顶点着色器中来做计算。

```
const vertexBuffers = beam.resource(VertexBuffers, {
  position: [
    -1, -1, 0, // vertex 0, bottom left
    0, 1, 0, // vertex 1, top middle
    1, -1, 0 // vertex 2, bottom right
  ],
  color: [
    1, 0, 0, // vertex 0, red
    0, 1, 0, // vertex 1, green
    0, 0, 1 // vertex 2, blue
  ]
})
复制代码
```

装顶点的 Buffer 通常会使用很紧凑的数据集。我们可以定义这份数据的一个子集或者超集来用于实际渲染，以便于减少数据冗余并复用更多顶点。为此我们需要引入 WebGL 中的 `IndexBuffer` 概念，它指定了渲染时用到的顶点下标：

> 这个例子里，每个下标都对应顶点数组里的 3 个位置。

```
const indexBuffer = beam.resource(IndexBuffer, {
  array: [0, 1, 2]
})
复制代码
```

最后我们就可以进入渲染环节啦。首先用 `beam.clear` 来清空当前帧，然后为 `beam.draw` 传入**一个着色器对象和任意多个资源对象**即可：

```
beam
  .clear()
  .draw(shader, vertexBuffers, indexBuffer)
复制代码
```

我们的 `beam.draw` API 是非常灵活的。如果你有多个着色器和多个资源，可以随意组合它们来链式地完成绘制，渲染出复杂的场景。就像这样：

```
beam
  .draw(shaderX, ...resourcesA)
  .draw(shaderY, ...resourcesB)
  .draw(shaderZ, ...resourcesC)
复制代码
```

别忘了还有个遗漏的地方：如何决定三角形的渲染算法呢？这是在 `MyShader` 变量里指定的。它其实是个着色器的 Schema，像这样：

```
import { SchemaTypes } from 'beam-gl'

const vertexShader = `
attribute vec4 position;
attribute vec4 color;
varying highp vec4 vColor;
void main() {
  vColor = color;
  gl_Position = position;
}
`
const fragmentShader = `
varying highp vec4 vColor;
void main() {
  gl_FragColor = vColor;
}
`

const { vec4 } = SchemaTypes
export const MyShader = {
  vs: vertexShader,
  fs: fragmentShader,
  buffers: {
    position: { type: vec4, n: 3 },
    color: { type: vec4, n: 3 }
  }
}
复制代码
```

这个 Beam 中的着色器 Schema，由顶点着色器字符串、片元着色器字符串，和其它 Schema 字段组成。非常粗略地说，着色器对每个顶点执行一次，而片元着色器则对每个像素执行一次。这些着色器是用 WebGL 标准中的 GLSL 语言编写的。在 WebGL 中，顶点着色器将 `gl_Position` 作为坐标位置输出，而片元着色器则将 `gl_FragColor` 作为像素颜色输出。还有名为 `vColor` 的 varying 变量，它会由顶点着色器传递到片元着色器，并自动插值。最后，这里的 `position` 和 `color` 这两个 attribute 变量，和前面 `vertexBuffers` 中的 key 相对应。这就是 Beam 用于自动化命令的约定了。

## API 进阶使用

相信一定有许多同学对这一设计的可用性还会有疑问，毕竟即便能按这套规则来渲染三角形，未必能证明它适合更复杂的应用呀。其实 Beam 已经实际应用在了我们内部的不同场景中，下面简单介绍一些更进一步的示例。对这些示例的详细介绍，都可以在笔者编写的 Beam 文档中查到。

### 渲染 3D 物体

我们刚渲染出的三角形，还只是 2D 图形而已。如何渲染出立方体、球体，和更复杂的 3D 模型呢？其实并不难，只要多一些顶点和着色器的配置就行。以用 Beam 渲染这个 3D 球体为例：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016df989b596~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



3D 图形同样由三角形组成，而三角形也仍然由顶点组成。之前，我们的顶点包含 **position** 和 **color** 属性。而对于 3D 球体，我们则需要使用 **position** 和 **normal** 属性。这个 normal 即为法向量，包含了球体在该顶点位置的表面朝向，这对光照计算十分重要。

不仅如此，为了将顶点从 3D 空间转换到 2D 空间，我们需要一个由矩阵组成的「照相机」。对每个传递到顶点着色器的顶点，我们都需要为其应用这些变换矩阵。这些矩阵对于并行运行的着色器来说，是全局唯一的。这就是 WebGL 中的 **uniforms** 概念了。`Uniforms` 也是 Beam 中的一种资源类型，包含着色器中的不同全局配置，例如相机位置、线条颜色、特效强度等。

因此要想渲染一个最简单的球，我们可以复用上例中的片元着色器，只需更新顶点着色器为如下所示即可：

```
attribute vec4 position;
attribute vec4 normal;

// 变换矩阵
uniform mat4 modelMat;
uniform mat4 viewMat;
uniform mat4 projectionMat;

varying highp vec4 vColor;

void main() {
  gl_Position = projectionMat * viewMat * modelMat * position;
  vColor = normal; // 将法向量可视化
}
复制代码
```

因为我们已经在着色器中添加了 uniform 变量，Schema 也需要相应地添加一个 `uniforms` 字段：

```
const identityMat = [1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1]
const { vec4, mat4 } = SchemaTypes

export const MyShader = {
  vs: vertexShader,
  fs: fragmentShader,
  buffers: {
    position: { type: vec4, n: 3 },
    normal: { type: vec4, n: 3 }
  },
  uniforms: {
    // The default field is handy for reducing boilerplate
    modelMat: { type: mat4, default: identityMat },
    viewMat: { type: mat4 },
    projectionMat: { type: mat4 }
  }
}
复制代码
```

然后我们就可以继续使用 Beam 中简洁的 API 了：

```
const beam = new Beam(canvas)

const shader = beam.shader(NormalColor)
const cameraMats = createCamera({ eye: [0, 10, 10] })
const ball = createBall()

beam.clear().draw(
  shader,
  beam.resource(VertexBuffers, ball.data),
  beam.resource(IndexBuffer, ball.index),
  beam.resource(Uniforms, cameraMats)
)
复制代码
```

这个示例的代码可以在 [Basic Ball](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam%2Fblob%2Fmaster%2Fgallery%2Fpages%2Fbasic-graphics%2Fbasic-ball.js) 中找到。

> Beam 是一个不以 3D 为目标设计的 WebGL 库，因此几何对象、变换矩阵、相机等概念并不属于它的一部分。为了方便使用，Beam 的示例中包含了一些相关的 Utils 代码，但别对它们要求太高啦。

### 添加动画

如何移动 WebGL 中的物体呢？你当然可以计算出运动后的新位置并更新 Buffer，但这可能很慢。另一种方式是直接更新上面提到的变换矩阵。这些矩阵都属于短小精悍，易于更新的 uniforms 资源。

通过 `requestAnimationFrame` API，我们很容易就能让上面的球体运动起来：

```
const beam = new Beam(canvas)

const shader = beam.shader(NormalColor)
const ball = createBall()
const buffers = [
  beam.resource(VertexBuffers, ball.data),
  beam.resource(IndexBuffer, ball.index)
]
let i = 0; let d = 10
const cameraMats = createCamera({ eye: [0, d, d] })
const camera = beam.resource(Uniforms, cameraMats)

const tick = () => {
  i += 0.02
  d = 10 + Math.sin(i) * 5
  const { viewMat } = createCamera({ eye: [0, d, d] })

  // 更新 uniform 资源
  camera.set('viewMat', viewMat)

  beam.clear().draw(shader, ...buffers, camera)
  requestAnimationFrame(tick)
}
tick() // 开始 Render Loop
复制代码
```

这里的 `camera` 变量是个 Beam 的 `Uniforms` 资源实例，它的数据以 key-value 的形式存储。你可以自由添加或更高不同的 uniform key。当 `beam.draw` 触发时，只有与着色器相匹配的 uniform 数据才会上传到 GPU。

这个示例的代码可以在 [Zooming Ball](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam%2Fblob%2Fmaster%2Fgallery%2Fpages%2Fbasic-graphics%2Fzooming-ball.js) 中找到。

> Buffer 资源同样可以通过类似的 `set()` 方法来更新，不过对于 WebGL 中较重的负载来说，这可能比较慢。

### 渲染图像

我们已经看到了 `VertexBuffers` / `IndexBuffer` / `Uniforms` 三种资源类型了。如果想渲染图像，那么我们还需要最后一种关键的资源类型，即 `Textures`。这方面最简单的示例，是带有这样贴图的 3D 盒子：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016df6ca5af0~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



对于需要纹理的图形，在 **position** 和 **normal** 之外，我们还需要一个额外的 **texCoord** 属性，以便于将图像对齐到图形的相应位置，这个值也会插值后传入片元着色器中。看看这时的顶点着色器吧：

```
attribute vec4 position;
attribute vec4 normal;
attribute vec2 texCoord;

uniform mat4 modelMat;
uniform mat4 viewMat;
uniform mat4 projectionMat;

varying highp vec2 vTexCoord;

void main() {
  vTexCoord = texCoord;
  gl_Position = projectionMat * viewMat * modelMat * position;
}
复制代码
```

以及新的片元着色器：

```
uniform sampler2D img;
uniform highp float strength;

varying highp vec2 vTexCoord;

void main() {
  gl_FragColor = texture2D(img, vTexCoord);
}
复制代码
```

现在我们需要为 Schema 添加 `textures` 字段：

```
const { vec4, vec2, mat4, tex2D } = SchemaTypes
export const MyShader = {
  vs: vertexShader,
  fs: fragmentShader,
  buffers: {
    position: { type: vec4, n: 3 },
    texCoord: { type: vec2 }
  },
  uniforms: {
    modelMat: { type: mat4, default: identityMat },
    viewMat: { type: mat4 },
    projectionMat: { type: mat4 }
  },
  textures: {
    img: { type: tex2D }
  }
}
复制代码
```

最后就是渲染逻辑了：

```
const beam = new Beam(canvas)

const shader = beam.shader(MyShader)
const cameraMats = createCamera({ eye: [10, 10, 10] })
const box = createBox()

loadImage('prague.jpg').then(image => {
  const imageState = { image, flip: true }
  beam.clear().draw(
    shader,
    beam.resource(VertexBuffers, box.data),
    beam.resource(IndexBuffer, box.index),
    beam.resource(Uniforms, cameraMats),
    // 这个 'img' 键用来与着色器相匹配
    beam.resource(Textures, { img: imageState })
  )
})
复制代码
```

这就是 Beam 中基础的纹理使用方式了。因为我们能直接控制图像着色器，在此基础上添加图像处理特效是很容易的。

这个示例的代码可以在 [Image Box](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam%2Fblob%2Fmaster%2Fgallery%2Fpages%2Fbasic-graphics%2Fimage-box.js) 中找到。

> 这里不妨将 `createBox` 换成 `createBall` 试试？

### 渲染多个物体

如何渲染多个物体呢？让我们看看 `beam.draw` API 的灵活性吧：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016e016080ad~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



要渲染多个球体和多个立方体，我们只需要两组 `VertexBuffers` 和 `IndexBuffer`，一组是球，另一组则是立方体：

```
const shader = beam.shader(MyShader)
const ball = createBall()
const box = createBox()
const ballBuffers = [
  beam.resource(VertexBuffers, ball.data),
  beam.resource(IndexBuffer, ball.index)
]
const boxBuffers = [
  beam.resource(VertexBuffers, box.data),
  beam.resource(IndexBuffer, box.index)
]
复制代码
```

然后在 for 循环里，我们就可以轻松地用不同的 uniform 配置来绘制它们了。只要在 `beam.draw` 前更新 `modelMat`，我们就可以更新该物体在世界坐标系中的位置，进而使其出现在屏幕上的不同位置了：

```
const cameraMats = createCamera(
  { eye: [0, 50, 50], center: [10, 10, 0] }
)
const camera = beam.resource(Uniforms, cameraMats)
const baseMat = mat4.create()

const render = () => {
  beam.clear()
  for (let i = 1; i < 10; i++) {
    for (let j = 1; j < 10; j++) {
      const modelMat = mat4.translate(
        [], baseMat, [i * 2, j * 2, 0]
      )
      camera.set('modelMat', modelMat)
      const resources = (i + j) % 2
        ? ballBuffers
        : boxBuffers

      beam.draw(shader, ...resources, camera)
    }
  }
}

render()
复制代码
```

这里的 `render` 函数以 `beam.clear` 开始，紧接着就可以跟随复杂的 `beam.draw` 渲染逻辑了。

这个示例的代码可以在 [Multi Graphics](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam%2Fblob%2Fmaster%2Fgallery%2Fpages%2Fbasic-graphics%2Fmulti-graphics.js) 中找到。

### 离屏渲染

在 WebGL 中可以使用 framebuffer object 来实现离屏渲染，从而将输出渲染到纹理上。Beam 目前有一个相应的 `OffscreenTarget` 资源类型，不过注意这一类型是不能扔进 `beam.draw` 的。

比如默认的渲染逻辑看起来像这样：

```
beam
  .clear()
  .draw(shaderX, ...resourcesA)
  .draw(shaderY, ...resourcesB)
  .draw(shaderZ, ...resourcesC)
复制代码
```

通过可选的 `offscreen2D` 方法，这一渲染逻辑可以轻松地这样嵌套在函数作用域里：

```
beam.clear()
beam.offscreen2D(offscreenTarget, () => {
  beam
    .draw(shaderX, ...resourcesA)
    .draw(shaderY, ...resourcesB)
    .draw(shaderZ, ...resourcesC)
})
复制代码
```

这样就可以将输出重定向到离屏的纹理上了。

这个示例的代码可以在 [Basic Mesh](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam%2Fblob%2Fmaster%2Fgallery%2Fpages%2Foffscreen%2Fbasic-mesh.js) 中找到。

### 其他渲染技术

对实时渲染来说，用于标准化渲染质感的基于物理渲染 (PBR) 和用于渲染阴影的 Shadow Mapping，是两种主要的进阶渲染技术。笔者在 Beam 中也实现了这两者的示例，例如上面出现过的 PBR 材质球：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016cb41d8cd2~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



这些示例省略了一些琐碎之处，相对更注重代码的可读性。可以看看这里：

- [Material Ball](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam%2Fblob%2Fmaster%2Fgallery%2Fpages%2F3d-models%2Fmaterial-ball.js) 展示了基础 PBR 材质球的渲染。
- [Basic Shadow](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam%2Fblob%2Fmaster%2Fgallery%2Fpages%2Foffscreen%2Fbasic-shadow.js) 展示了 Shadow Mapping 的示例。

如前文所言，目前 [稿定设计 Web 版](https://link.juejin.cn/?target=https%3A%2F%2Fgaoding.com) 的 3D 文字特性，也是从 Beam 的 PBR 能力出发来实现的。像这样的 3D 文字：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016e1d6f4969~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



或者这样：



![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/11/25/16ea016e51663150~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



它们都是用 Beam 来渲染的。当然，Beam 只负责直接与 WebGL 相关的渲染部分，在其之上还有我们定制之后，嵌入平面编辑器中使用的 3D 文字渲染器，以及文字几何变换相关的算法。这些代码涉及我们的一些专利，并不会随 Beam 一起开源。其实，基于 Beam 很容易实现自己定制的专用渲染器，从而实现面向特定场景的优化。这也是笔者对这样一个 WebGL 基础库的预期。

在 Beam 自带的示例中，还展示了基于 Beam 实现的这些例子：

- 物体 Mesh 加载
- 纹理配置
- 经典光照算法
- 可串联的图像滤镜
- 深度纹理可视化
- 基础的粒子效果
- WebGL 扩展配置
- 上层 Renderer 封装

[Beam](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fdoodlewind%2Fbeam) 已经开源，欢迎 PR 提供新的示例哦 :)

## 致谢与总结

Beam 的实现历程里，和 at 工业聚在 API 设计层面的交流给了笔者很多启发。公司内外不少前辈的指点，也在笔者面临关键决策时很有帮助。最终这套方案能够落地，更离不开组内前端同学们支持下最为重要的，**大家大量的细节工作**。

其实在接下 3D 文字的需求前，笔者并没有比画一堆立方体更复杂的 WebGL 经验。但只要以基础出发来学习，短短几个月里，就足够在满足产品需求的基础上熟悉 WebGL，顺便沉淀出这样的轮子了。所以其实没必要以「这个在我能力范围外」为理由来为自己设限，把自己束缚在某个舒适区内。作为工程师，我们能做的事还有很多！

而对于 Beam 自身的存在必要性而言，至少在国内，笔者确实还没发现在 WebGL 基础库的这个细分定位上，有比它更符合理想化设计的开源产品。这里真的不是说国内技术实力不行，像沈毅大神的 ClayGL 和谢光磊大神的 G3D 就都非常棒。区别之处在于，它们解决的其实是比 Beam 更高层次、更贴近普通开发者的问题。拿它们和 Beam 相比较，就像拿 Vue 和简化的 React Reconciler 相比较一样。

越做越发现，这是个相当小众的领域。这意味着这样的技术产品，可能很难获得社区主流群体的尝试与认可。

可是，有些最后绕不开的事，总有人要去做呀。

> 我主要是个前端开发者。如果你对 Web 结构化数据编辑、WebGL 渲染、Hybrid 应用开发，或者计算机爱好者的碎碎念感兴趣，欢迎关注我或我的公众号 `color-album` 噢 :)

分类：

[前端](https://juejin.cn/frontend)

标签：

[JavaScript](https://juejin.cn/tag/JavaScript)[WebGL](https://juejin.cn/tag/WebGL)