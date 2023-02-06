# [webpack 打包后如何调用JS自定义函数？](https://segmentfault.com/q/1010000012739169)

## 问题

比如有一个JS文件: `assets/js/common.js`内容如下：

```isbl
function warning(){
    alert('FF')
}
```

在webpack 文件中引入：

```sml
mix.js('assets/js/common.js','public/js');
```

html中引入生成的文件 `public/js/app.js`，但如何在这个html中调用这个 `warning()` 方法？
直接调用提示undefined不存在

## 解决

webpack打包后，在文件定义的变量属于内部变量。也就是说webpack把各个文件封装。。。它让你在不能像

```dust
<script src='1.js'></script>
<script> 
    function balabala(){}  //1.js中的函数 
</script>
```

这样使用webpack打包生成js里的东西。
有兴趣的话(你需要你个好的编译器..)，你可以查一查webpack生成的js中，你的warning被不知道多少个括号装起来了。

------

你的解决方式是给warning()定义的时候，定义成全局变量，也就是

```isbl
window.warning = function(){
    alert('FF')
}
```

这样你就可以在html文件中的script标签中使用了

[回复](https://segmentfault.com/q/1010000012739169/###)

[**util**](https://segmentfault.com/u/util)：

感觉这样好麻烦啊~

[回复](https://segmentfault.com/q/1010000012739169/###)2018-01-08

[**秋水白**](https://segmentfault.com/u/qiushui_59fbb574e4976)：

如果要在你.html文件里用，换个创建函数的方式就好了window.balabala

[回复](https://segmentfault.com/q/1010000012739169/###)2018-01-08