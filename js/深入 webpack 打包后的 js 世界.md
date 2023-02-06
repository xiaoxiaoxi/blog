# 深入 webpack 打包后的 js 世界

[![img](https://p9-passport.byteacctimg.com/img/user-avatar/bba4797aafab5c1da066deb9952a23e0~300x300.image)](https://juejin.cn/user/1521379823583790)

[叶华春 ![lv-1](https://lf3-cdn-tos.bytescm.com/obj/static/xitu_juejin_web/636691cd590f92898cfcda37357472b8.svg)](https://juejin.cn/user/1521379823583790)

2019年07月03日 14:24 · 阅读 4108

关注

## 前言

在现代主流的前端项目开发中，几乎总能找到 webpack 的影子，它似乎已经成了现今前端开发中不可或缺的一部分。

下图是 webpack 官网首页，它生动形象的展现了 webpack 的核心功能：将一堆依赖关系复杂的模块打包成整齐有序的静态资源。



![webpack](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/7/3/16bb66fd0c1c8073~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



webpack 的出现加上现成脚手架的支持，让我们可以集中精力在项目开发上，而无需过多关注打包过程和结果。

可是，你是否好奇过，webpack 打包后的 js 代码是如何做到有序加载执行的？

回忆一下，我们在使用 webpack 的项目中，任何资源都可以被视作模块（只要有对应的 loader 支持解析），而这时模块（module）的载体是文件。但在项目打包后，模块的载体变成了函数，也被称为模块函数（module function），而文件则成了 chunk（块）的载体。所谓 chunk，是 webpack 中的一个概念，是由若干个模块组成的一个集合，一个 chunk 往往对应着一个文件。

实际上，要回答上面提出的问题，就要搞清楚打包后模块与模块，chunk 与 chunk，以及模块与 chunk 之间的关系。所以，下面我们将从 模块 和 chunk 这两个维度展开这篇文章。

## 模块

由于模块是资源加载中的最小单位，所以我们从最简单的模块加载开始。

下面是一个基础的 webpack4 配置文件。

```
// webpack.config.js
const path = require('path')

module.exports = {
  mode: 'production',
  entry: {
    main: './src/main.js'
  },
  output: {
    filename: '[name].js',
    chunkFilename: '[name].[contenthash:8].js',
    path: path.resolve(__dirname, 'dist')
  },
  optimization: {
    // 为了方便阅读理解打包后的代码，关闭代码压缩和模块合并
    minimize: false,
    concatenateModules: false
  }
}
复制代码
```

在执行构建命令 `npm run build` 后，项目中会生成一个 dist 文件夹，里面包含了一个 main.js 文件，下面是文件中的内容。（本文所有的示例代码为了聚焦重点，忽略掉了部分暂时无关的代码，避免加重读者阅读负担）

```
(function(modules) { // webpackBootstrap
    // 用于缓存已加载模块的地方
    var installedModules = {};

    // 用于加载模块的 require 函数
    function __webpack_require__(moduleId) { ... }

    // 加载入口模块（假设入口模块 id 为0）
    return __webpack_require__(0)
})([...])
复制代码
```

上面代码的实质是一个立即调用函数表达式（IIFE），其中的函数部分叫做 webpackBootstrap，传入的实参是一个包含模块函数的数组或对象。

### webpackBootstrap

下面是 bootstrap 的英文含义：

> A technique of loading a program into a computer by means of a few initial instructions which enable the introduction of the rest of the program from an input device.

翻译过来就是一种通过一些初始指令将程序加载到计算机中的技术，该初始指令使得能够从输入设备引入程序的其余部分。

如果还是不太理解的话，可以简单的将其理解成控制中心，负责一切事物的启动、调度、执行等。

在 webpackBootstrap 中，定义了一个模块缓存对象（installedModules）用于存放已加载模块，以及一个模块加载函数（`__webpack_require__`）用于获取对应 id 的模块，最后加载入口模块以启动整个程序。

下面我们重点来讲一下模块的加载。

```
// 加载模块
function __webpack_require__(moduleId) {
  // 检查缓存中是否有该模块，若有，则直接返回
  if (installedModules[moduleId]) {
    return installedModules[moduleId].exports
  }

  // 初始化一个新模块，并且保存到缓存中
  var module = installedModules[moduleId] = {
    i: moduleId, // 模块名
    l: false, // 布尔值，表示该模块是否加载完毕
    exports: {} // 模块的输出对象，包含了模块输出的各个接口
  }

  // 执行模块函数，并传入三个实参：模块本身、模块的输出对象、加载函数，同时定义 this 值为模块的输出对象
  modules[moduleId].call(
    module.exports,
    module,
    module.exports,
    __webpack_require__
  )

  // 标记模块为已加载状态
  module.l = true

  // 返回模块的输出对象
  return module.exports
}
复制代码
```

上面的代码说明，编译后模块的加载遵循 CommonJS 规范。不过，CommonJS 模块规范不是同步加载模块，不适用于浏览器端吗？实际上，这是因为 webpack 编译后的代码确保了在对模块进行加载时，模块已经从服务器下载好了，因此并没有同步请求导致的阻塞问题。至于这个问题具体是如何解决的，会在下面的 chunk 章节作出解释。

下面是模块加载的流程图。



![模块加载流程](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2019/7/3/16bb6702c95cc83b~tplv-t2oaga2asx-zoom-in-crop-mark:1304:0:0:0.awebp)



不过，这里有几点值得注意：

- 同一个模块如果加载多次，将只执行一次，所以需要对加载过的模块进行缓存。
- 在初始化新模块后，新模块被立即保存到缓存中，而不是在模块加载完成后。这其实是为了解决模块间循环加载（circular dependency）问题，即 a 模块依赖 b 模块，b 模块依赖 a 模块。这样一来，未执行完毕的模块被再次加载时，会在检查缓存时直接返回模块的输出对象（该输出对象可能并不包含模块全部的输出接口），以避免无限循环。
- 在 CommonJS 模块中，顶层的 this 值为 `module.exports`，因此利用 call 函数定义模块函数的 this 值为 `module.exports`。但是在 ES6 模块中，顶层的 this 为 undefined，所以在编译时 this 就被转换成了 undefined。

### 模块函数

那么执行模块函数时究竟做了什么呢？简单来说，就是将被加载模块的输出接口添加到输出对象上。

下面我们通过一个简单的例子来看看模块函数（由于 webpack 官方推荐使用 ES6 模块语法，因此示例中使用 ES6 中的 import/export）。

```
// src/lib.js
export let counter = 0

export function plusOne() {
  counter++
}

// src/main.js（入口模块）
import { counter, plusOne } from './lib'

console.log(counter)

plusOne()
console.log(counter)
复制代码
```

下面是 webpack 打包编译后的模块函数。

```
（function(modules) {
  ...
  // 步骤1：加载入口模块
  return __webpack_require__(1)
}）(
  [
    /* moduleId: 0 */
    function(module, __webpack_exports__, __webpack_require__) {
      // ES6模块默认采用严格模式
      'use strict'

      // 步骤1.1.1：在输出对象上定义输出的各个接口
      __webpack_require__.d(__webpack_exports__, 'a', function() {
        return counter
      })
      __webpack_require__.d(__webpack_exports__, 'b', function() {
        return plusOne
      })

      // 步骤1.1.2：声明定义输出接口的值
      let counter = 0

      function plusOne() {
        counter++
      }
    },
    /* moduleId: 1 */
    function(module, __webpack_exports__, __webpack_require__) {
      'use strict'
      // 步骤1.1：加载lib.js模块，并返回其输出对象
      var _lib__WEBPACK_IMPORTED_MODULE_0__ = __webpack_require__(0)
      // _lib__WEBPACK_IMPORTED_MODULE_0__ = {
      //   get a() { return couter },
      //   get b() { return pluseOne }
      // }

      // 步骤1.2：调用输出对象上的输出接口
      console.log(_lib__WEBPACK_IMPORTED_MODULE_0__[/* counter */ 'a'])

      Object(_lib__WEBPACK_IMPORTED_MODULE_0__[/* plusOne */ 'b'])()
      console.log(_lib__WEBPACK_IMPORTED_MODULE_0__[/* counter */ 'a'])
    }
  ]
)

复制代码
```

上面代码中，ES6 模块文件被编译成了 CommonJS 规范的模块函数。为了保持 ES6 模块语法的特性，编译后的代码变得有些晦涩难懂。其中有几点比较费解：

1. `__webpack_require__.d` 函数是用来干什么的？

   这个函数是为了在输出对象上定义输出的各个接口。可是简单的对象属性赋值不就可以完成这个任务吗？这是因为**ES6 模块输出的是值的只读引用**。

   下面是 `__webpack_require__.d` 的实现。

   ```
   __webpack_require__.d = function(exports, name, getter) {
     // __webpack_require__.o 是用于判断输出对象上是否已存在同名的输出接口
     if (!__webpack_require__.o(exports, name)) {
       Object.defineProperty(exports, name, { enumerable: true, get: getter })
     }
   }
   复制代码
   ```

   上面的代码表明在输出 ES6 模块的接口时，会使用 `Object.defineProperty` 方法来定义输出对象上的属性，而且只定义属性的 getter（取值器函数），以此实现了输出接口为只读。再通过属性的 getter 配合闭包实现了输出接口为值的引用。

2. 为什么统一在模块函数顶部定义输出接口（除 `export default` 的一些特殊场景以外，如 `export default 1` 这样没有明确指定输出接口名的）？

   这是因为 **ES6 模块是编译时输出接口**，相比之下，CommonJS 模块是运行时加载。这两者间的区别在模块间循环加载问题中会得到体现。因此为了模拟 ES6 模块的这个特性，需要在模块加载所依赖的模块或执行其他操作前，先定义输出接口名。

3. 为什么在消费 lib 模块的输出接口时，需要每次都从输出对象上取（如步骤1.2中消费 couter 值），而不像原代码中输出接口是独立的（如原代码中的 couter 变量）？

   这是由于输出对象上的属性实际上是一个 getter 函数，如果将该属性值取出单独声明一个变量，便失去闭包的效果，无法追踪被加载模块中输出接口值的变动，也就失去了输出接口为值的引用这一 ES6 模块的特性。以上面示例代码举例，正常情况下控制台依次输出0和1，但如果将编译后的输出接口值赋予一个新变量，控制台则会输出两次0。

## chunk （块）

如果一个项目的代码体积变大，那么将所有 js 代码打包到一个文件中必然会遇到性能瓶颈，导致资源加载时间过长。这时候，webpack 的 split chunks 技术就派上了用场。可以根据不同的分包优化策略，将模块拆分到不同的 chunk 文件中。

### 异步 chunk（async chunk）

对于一些访问频率较低的路由或使用频率较低的组件可以通过懒加载拆分为异步 chunk。

异步 chunk 可以通过调用 `import()` 方法动态加载模块得到。下面我们改造一下 main.js 文件，以懒加载 lib 模块。

```
// src/main.js
import('./lib').then((lib) => {
  console.log(lib.counter)

  lib.plusOne()
  console.log(lib.counter)
})
复制代码
```

下面是重新构建打包后的 main.js 文件（只展示了新增的和发生变更的代码）。

```
// dist/main.js
(function(modules) {
  // chunk 下载完毕后执行的函数
  function webpackJsonpCallback(data) { ... }

  // 用于标记各个 chunk 加载状态的对象
  // undefined：chunk 未加载
  // null：chunk preloaded/prefetched
  // Promise：chunk 正在加载
  // 0：chunk 已加载
  var installedChunks = {
    0: 0
  }

  // 获取 chunk 的请求地址（url），包含了 chunk 名及 chunk 哈希
  function jsonpScriptSrc(chunkId) {
    return __webpack_require__.p + "" + ({}[chunkId]||chunkId) + "." + {"1":"3215c03a"}[chunkId] + ".js"
  }

  // 获取 chunk
  __webpack_require__.e = function requireEnsure(chunkId) { ... }

  // chunk 的公共路径（public path），即 webpack 配置中的 output.publicPath
  __webpack_require__.p = "";

  // 围绕 webpackJsonp 的一系列操作，会在下面做详细介绍
  var jsonpArray = window["webpackJsonp"] = window["webpackJsonp"] || [];
  var oldJsonpFunction = jsonpArray.push.bind(jsonpArray);
  jsonpArray.push = webpackJsonpCallback;
  jsonpArray = jsonpArray.slice();
  for(var i = 0; i < jsonpArray.length; i++) webpackJsonpCallback(jsonpArray[i]);
  var parentJsonpFunction = oldJsonpFunction;

  return __webpack_require__(0);
})([
  /* 0 */
  (function(module, exports, __webpack_require__) {
    __webpack_require__.e(/* import() */ 1).then(__webpack_require__.bind(null, 1)).then((lib) => {
      console.log(lib.counter)

      lib.plusOne()
      console.log(lib.counter)
    })
  })
])
复制代码
```

#### `__webpack_require__.e`

上面的代码中，入口模块中的 `import('./lib')` 被编译为了 `__webpack_require__.e(1).then(__webpack_require__.bind(null, 1))`， 这实际上等价于下面的代码。

```
__webpack_require__.e(1)
  .then(function() {
    return __webpack_require__(1)
  })
复制代码
```

上面的代码由两部分组成，前半段的 `__webpack_require__.e(1)` 是用来异步加载 chunk 的，后半段传入 then 方法中的回调函数是用来同步加载 lib 模块的。

这就解决了 CommonJS 规范中**同步加载模块**会在浏览器端导致的执行堵塞问题。

```
// 获取 chunk
__webpack_require__.e = function requireEnsure(chunkId) {
  var promises = [];

  // 利用 JSONP 下载 js chunk
  var installedChunkData = installedChunks[chunkId];
  // 0代表该 chunk 已加载完毕
  if(installedChunkData !== 0) {

    if(installedChunkData) { // chunk 正在加载中
      promises.push(installedChunkData[2]);
    } else {
      // 在 chunk 缓存中更新 chunk 状态为正在加载中，并缓存 resolve、reject、promise
      var promise = new Promise(function(resolve, reject) {
        installedChunkData = installedChunks[chunkId] = [resolve, reject];
      });
      promises.push(installedChunkData[2] = promise);

      // 开始准备下载 chunk
      var script = document.createElement('script');
      var onScriptComplete;

      script.charset = 'utf-8';
      script.timeout = 120;
      if (__webpack_require__.nc) {
        script.setAttribute("nonce", __webpack_require__.nc);
      }
      script.src = jsonpScriptSrc(chunkId);

      // 在堆栈展开之前创建 error 以便稍后获得有用的堆栈跟踪
      var error = new Error();
      // chunk 下载完成后（成功或异常）的回调函数
      onScriptComplete = function (event) {
        // 防止 IE 浏览器下内存泄漏
        script.onerror = script.onload = null;
        clearTimeout(timeout);
        var chunk = installedChunks[chunkId];
        if(chunk !== 0) {
          if(chunk) {
            var errorType = event && (event.type === 'load' ? 'missing' : event.type);
            var realSrc = event && event.target && event.target.src;
            error.message = 'Loading chunk ' + chunkId + ' failed.\n(' + errorType + ': ' + realSrc + ')';
            error.name = 'ChunkLoadError';
            error.type = errorType;
            error.request = realSrc;
            // reject(error)
            chunk[1](error);
          }
          installedChunks[chunkId] = undefined;
        }
      };
      // 处理请求超时
      var timeout = setTimeout(function(){
        onScriptComplete({ type: 'timeout', target: script });
      }, 120000);
      // 处理请求成功及异常
      script.onerror = script.onload = onScriptComplete;
      // 发起请求
      document.head.appendChild(script);
    }
  }
  return Promise.all(promises);
};
复制代码
```

下面是`__webpack_require__.e`的执行流程：

1. 初始化 promises 变量，用于处理各个 chunk 的异步加载流程（虽然上面示例中只需要处理一个 js chunk，但是有些 js 模块依赖于 css 文件，因此在加载 js chunk 的同时也会加载其依赖的 css chunk，需要处理多个 chunk 的异步加载，所以该变量为一个数组）。
2. 判断 js chunk 是否已加载，如果 chunk 已加载，直接跳到第6步，否则继续往下执行。
3. 判断 chunk 是否正在加载，如果是，将 chunk 缓存（installedChunks）中该 chunk 保存的数组中的 promise 实例添加到 promises 数组中，然后跳到第6步，否则继续往下执行。
4. 初始化一个 promise 实例用于处理 chunk 的异步加载流程，并且将由 Promise 的 resolve 和 reject 函数以及 promise 实例本身组成的数组（即 `[resolve, reject, promise]`）保存到 chunk 缓存中，再将 promise 实例添加到 promises 数组中。
5. 开始准备下载 chunk，包括创建 script 标签，设置 script 的 src、timeout 等一些属性，处理 script 的请求成功、失败、超时事件，最后添加 script 到 document 完成请求的发送。
6. 执行并返回 `Promise.all(promises)`，等所有异步 chunks 都加载成功后，再触发 then 方法中的回调函数（即加载 chunk 中包含的模块）。

或许有人会感到困惑，为什么没有在 onScriptComplete 中 `chunk === 0` 时执行 resolve 函数？就像下面这样：

```
onScriptComplete = function (event) {
  ...
  var chunk = installedChunks[chunkId];
  if(chunk !== 0) {
    if(chunk) {
      ...
      // reject(error)
      chunk[1](error);
    }
    installedChunks[chunkId] = undefined;
  } else { // chunk === 0
    // resolve()
    chunk[0]()
  }
};
复制代码
```

这个问题的实质是 chunk 的异步加载流程什么时候才算结束？是否 chunk 下载完成后就算结束了？实际上，js chunk 的加载包含两个部分：下载 chunk 文件和执行 chunk 代码，只有当两者都完成后，该 chunk 才算加载完成。因此，resolve 被保存到了 chunk 缓存中，待 chunk 代码执行完毕后再执行 resolve 函数，结束掉异步加载流程。虽然 script 的 load 事件是在其下载并执行完毕后才触发，但是 load 事件只关心下载本身，即使 script 在执行过程中抛出异常，依然会触发 load 事件。

#### webpackJsonpCallback

当 js chunk 下载成功后，就会开始执行代码，下面是 lib.js 模块打包得到的 chunk。

```
// dist/1.3215c03a.js
(window["webpackJsonp"] = window["webpackJsonp"] || []).push([[1],[
  /* 0 */,
  /* 1 */
  (function(module, __webpack_exports__, __webpack_require__) {

    "use strict";
    __webpack_require__.d(__webpack_exports__, "counter", function() { return counter; });
    __webpack_require__.d(__webpack_exports__, "plusOne", function() { return plusOne; });
    let counter = 0

    function plusOne() {
      counter++
    }

  })
]]);
复制代码
```

上面的代码看上去很简单，只有两步操作，一个是初始化 `window["webpackJsonp"]` 为数组（若之前未被初始化）， 另一个是通过 push 操作将一个数组添加到 `window["webpackJsonp"]` 数组中（表达并不严谨，详情见下文）。其中作为实参的数组又由两个数组构成，第一个数组是 chunkId 的集合（正常情况下，该数组只包含当前 chunkId。但在分包策略有误的情况下，该数组可能包含多个 chunkId），第二个数组则是模块函数的集合。

但是，原生的 push 操作只能简单的将 chunk 中的数据添加到数组里。那 webpack 究竟是在哪里对数据做的处理？又是如何做的处理？

如果还有印象的话，在上面的 webpackBootstrap 中有一段围绕 `window["webpackJsonp"]` 数组的操作。

```
var jsonpArray = window["webpackJsonp"] = window["webpackJsonp"] || [];
var oldJsonpFunction = jsonpArray.push.bind(jsonpArray);
// 将 window["webpackJsonp"].push 方法替换为 webpackJsonpCallback 函数
jsonpArray.push = webpackJsonpCallback;
jsonpArray = jsonpArray.slice();
// 对之前已加载的全部初始 chunk 中的数据调用 webpackJsonpCallback
for(var i = 0; i < jsonpArray.length; i++) webpackJsonpCallback(jsonpArray[i]);
// 将 window["webpackJsonp"] 数组原生的 push 方法赋给 parentJsonpFunction 变量
var parentJsonpFunction = oldJsonpFunction;
复制代码
```

从上面代码可以看出，所有的 chunks 中的数据（除 webpackBootstrap 所在的 chunk 以外）都是通过 JSONP 的形式（即调用 webpackJsonpCallback）加载进来并做处理的，但在 webpackBootstrap 所在的 chunk 未加载好的之前，webpackJsonpCallback 还未被声明定义，因此便将数据都先暂时保存在 `window["webpackJsonp"]` 数组里，待其加载好之后，先将 `window["webpackJsonp"]` 数组的 push 方法替换为 webpackJsonpCallback 函数（这样一来，之后加载的 chunk 虽然调用的是 push 方法，但实际上是直接调用 webpackJsonpCallback 函数处理数据），再将先前保存在 `window["webpackJsonp"]` 数组里的数据依次调用 webpackJsonpCallback。

```
function webpackJsonpCallback(data) {
  var chunkIds = data[0];
  var moreModules = data[1];

  var moduleId, chunkId, i = 0, resolves = [];
  // 取出各个异步 chunk 所对应的 promise 的 resolve 函数，并在 chunk 缓存中标记 chunk 状态为已加载
  for(;i < chunkIds.length; i++) {
    chunkId = chunkIds[i];
    if(installedChunks[chunkId]) {
      resolves.push(installedChunks[chunkId][0]);
    }
    installedChunks[chunkId] = 0;
  }
  // 将 chunk 中包含的模块都添加到 webpackBootstrap 的 modules 对象中
  for(moduleId in moreModules) {
    if(Object.prototype.hasOwnProperty.call(moreModules, moduleId)) {
      modules[moduleId] = moreModules[moduleId];
    }
  }
  // 利用 window["webpackJsonp"] 数组原生的 push 方法将 chunk 中的数据添加到 window["webpackJsonp"] 中
  if(parentJsonpFunction) parentJsonpFunction(data);

  // 异步 chunks 加载成功，执行 resolve 函数来 fulfill 各个 chunk 对应的 promise，触发 then 中的回调函数
  while(resolves.length) {
    resolves.shift()();
  }
};
复制代码
```

webpackJsonpCallback 函数主要对 chunk 中的数据做了两个处理：缓存、结束异步加载流程。

缓存包含两个层面：一个是对 chunk 加载状态的缓存，以避免对同一 chunk 发送多次请求，另一个是对模块函数的缓存，以便后期对模块的加载。

结束 chunk 的异步加载流程，实际就是执行 chunk 缓存中的 resolve 函数。

### 初始 chunk（initial chunk）

对于网站初始阶段需要加载的模块，可以根据模块的体积大小、共用率、更新频率，拆分为核心基础类库、UI 组件库、业务代码等多个初始 chunk。

为了得到多个初始 chunk，调整一下 main.js 文件和 webpack.config.js 配置。

```
// src/main.js
import * as _ from 'lodash'

const arr = [1, 2]
console.log(_.concat(arr, 3, [4]))

// webpack.config.js（基于上面的 webpack 配置）
module.exports = {
  ...
  optimization: {
    ...
    splitChunks: {
      cacheGroups: {
        vendors: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all',
          priority: 10,
        },
      }
    }
  }
}
复制代码
```

上面代码中，main.js 模块依赖了 lodash 库，并将 lodash 库拆分到一个单独的 chunk 中，所以在 webpack 配置的 optimization 对象中增加了 splitChunks 配置，用于将 lodash 库拆分到名为 vendors 的 chunk 中。

下面是打包后 webpackBootstrap 中增加的代码。

```
(function(modules) { // webpackBootstrap
  function webpackJsonpCallback(data) {
    ...
    var executeModules = data[2];
    // 如果加载的 chunk 中有入口模块，则将其添加到 deferredModules 数组
    deferredModules.push.apply(deferredModules, executeModules || []);

    return checkDeferredModules();
  }

  // 检查入口模块所依赖的 chunk 是否加载完成，如果是，则加载入口模块，否则不执行任何操作
  function checkDeferredModules() {
    var result;
    // 遍历所有入口模块
    for(var i = 0; i < deferredModules.length; i++) {
      var deferredModule = deferredModules[i];
      var fulfilled = true;
      // 检查入口模块所依赖的全部 chunk 是否加载完成
      for(var j = 1; j < deferredModule.length; j++) {
        var depId = deferredModule[j];
        if(installedChunks[depId] !== 0) fulfilled = false;
      }
      // 如果入口模块依赖的全部 chunk 都加载完成，则加载入口模块
      if(fulfilled) {
        deferredModules.splice(i--, 1);
        result = __webpack_require__(deferredModule[0]);
      }
    }
    return result;
  }

  var deferredModules = [];

  // 将入口模块添加到 deferredModules 数组
  // 数组中第一个元素为入口模块 id，后面的元素都是入口模块依赖的初始 chunk 的 id
  deferredModules.push([1,1]);

  return checkDeferredModules();
})(...)
复制代码
```

原来只有一个初始 chunk 时， chunk 中包含了初始阶段所需的全部模块，所以当其下载好后就可以直接加载入口模块。但当模块被拆分到多个初始 chunk 中的时候，必须得等全部初始 chunk 都加载完成，全部初始阶段所需的模块都准备好后，才可以开始加载入口模块。因此，唯一不同的是入口模块的加载时机被 **defer（延迟）** 了。

所以在上面代码中，webpackBootstrap 函数和 webpackJsonpCallback 函数都在最后调用了 checkDeferredModules 函数，确保所有 chunk 在加载完成后都会检查是否有入口模块已经满足了要求（即其依赖的全部初始 chunk 都已加载完成），如果有入口模块满足了，则开始加载该入口模块。

## 小结

本文实际上就解答了一个问题：webpack 打包后的 js 代码是如何运行的？答案的核心有两点：模块的加载和 chunk 的加载。前者同步阻塞，后者异步非阻塞。当你清楚如何将两者和谐的配合在一起时，也就离完整的答案不远了。