# [Threejs]三种坐标系位置数据的转换

webGL中主要有6种坐标系．接下来看看如何在以下三种坐标系之间进行坐标数据的转换：屏幕坐标系，标准坐标系，世界坐标系．

- 屏幕坐标系和标准设备坐标系

先来了解一下这两个坐标系的定义，具体如下图所示：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20191029091856426.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21veGlhb21vbW8=,size_16,color_FFFFFF,t_70)


可以看到屏幕坐标系的起始点(0,0)在左上角，而标准坐标系的起始点在canvas中心处.

- 假设3D画布的大小填满window

假如我们要通过鼠标来操控3D画布内的场景对象，需要将鼠标的坐标位置转换为3D世界坐标，具体流程为屏幕坐标->标准坐标->世界坐标,

具体代码示例如下：

 ```
    import {Vector3} from 'three';
 
    onMouseClicked() {
         const mouseX = event.clientX;//鼠标单击坐标X
         const mouseY = event.clientY;//鼠标单击坐标Y
 
         // 屏幕坐标转标准设备坐标
         const x = ( mouseX / window.innerWidth ) * 2 - 1;
         const y = -( mouseY / window.innerHeight ) * 2 + 1;
         //标准设备坐标(z=0.5这个值并没有一个具体的说法)
         const stdVector = new Vector3(x, y, 0.5);
 
         // 通过unproject方法，可以将标准设备坐标转世界坐标
         const worldVector = stdVector.unproject(camera);
         // 进行剩下操作，比如判断鼠标是否选中某个物体
     }
     // 窗口鼠标单击
     // window.addEventListener('click',onMouseClicked);
 ```

反过来，如果要求出物体响应的屏幕坐标，世界坐标->标准坐标->屏幕坐标，那么可以这样:

```
// const box = ...
const worldVector = new Vector3(
    box.position.x,
    box.position.y,
    box.position.z
);
//世界坐标转标准设备坐标
const stdVector = worldVector.project(camera);
const a = window.innerWidth / 2;
const b = window.innerHeight / 2;
//标准设备坐标转屏幕坐标x,y
const x = Math.round(stdVector.x * a + a);
const y = Math.round(-stdVector.y * b + b);
```

假设3D画布的只是window中的一个窗口，比如某个div内的canvas这时候只要获取到canvas所在的div的宽高及左上位移数据就可以计算了，具体如下：

    const mouseX = event.clientX;//鼠标单击坐标X
    const mouseY = event.clientY;//鼠标单击坐标Y
    const rect = someDiv.getBoundingClientRect();
    const x = ((mouseX - rect.left) / someDiv.clientWidth) * 2 - 1;
    const y = - ((mouseY - rect.top) / someDiv.clientHeight) * 2 + 1;
    const stdVector = new Vector3(x, y, 0.5);
    // 通过unproject方法，可以将标准设备坐标转世界坐标
    const worldVector = stdVector.unproject(camera);
————————————————
版权声明：本文为CSDN博主「moxiaomomo」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/moxiaomomo/article/details/102792861