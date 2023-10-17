#### 1.渲染上下文

```bash
Canvas标签起初只是创造了一个固定大小的画布，它公开了一个或多个渲染上下文，而我们想对它进行绘制就需要找到渲染上下文。
Canvas标签提供了一个方法叫：getContext() ，通过它我们可以获得渲染上下文和绘画功能。
```

##### `getContext`方法是有一个接收参数，它是绘图上下文的类型，可能的参数有:

- `2d`：建立一个二维渲染上下文。这种情况可以用` CanvasRenderingContext2D()`来替换`getContext('2d')`。

- `webgl`（或 `experimental-webgl`）： 创建一个 `WebGLRenderingContext `三维渲染上下文对象。只在实现`WebGL` 版本1(`OpenGL ES 2.0`)的浏览器上可用。

- `webgl2`（或 `experimental-webgl2`）：创建一个 `WebGL2RenderingContext `三维渲染上下文对象。只在实现` WebGL `版本2 (`OpenGL ES 3.0`)的浏览器上可用。

- `bitmaprenderer`：创建一个只提供将canvas内容替换为指定`ImageBitmap`功能的`ImageBitmapRenderingContext`。

#### 2.绘制形状

```js
moveTo(x, y) //设置初始位置， 参数为初始位置的x，y坐标。
lineTo(x, y) //绘制一条直线从初始位置到指定位置的一条直线
stroke(x, y) //通过线条来绘制图形轮廓

//绘制三角形
let canvas = document.getElementById('canvas');
console.log(canvas);
 if (canvas.getContext) {
    let ctx = canvas.getContext('2d');
    ctx.moveTo(50, 50);
    ctx.lineTo(100, 100);
    ctx.lineTo(100, 50);
    ctx.lineTo(50, 50);
    ctx.stroke()
 }

//绘制矩形  Canvas API 给提供了三种绘制矩形的方法 x,y起始坐标 矩形的宽高
strokeRect(x, y, width, height) 绘制一个矩形的边框
fillRect(x, y, width, height) 绘制一个填充的矩形
clearRect(x, y, width, height) 清除指定矩形区域，让清除部分完全透明。

//绘制圆弧和圆
绘制圆弧或者圆，使用的方法是：arc(x, y, radius, startAngle, endAngle, anticlockwise)。x和Y为圆心的坐标，radius为半径，startAngle为圆弧或圆的开始位置，endAngle为圆弧或圆的结束位置，anticlockwise是绘制的方向（不写默认为false，从顺时针方向）
在画弧的时候，arc()函数中角的单位是弧度而不是角度。角度换算为弧度的表达式为：弧度=(Math.PI/180)*角度。
var ctx = canvas.getContext('2d');
// 绘制一段圆弧
ctx.arc(60, 60, 50, 0, Math.PI, false);
ctx.stroke();
// 绘制一个圆弧
ctx.arc(200, 60, 50, 0, Math.PI*2, false);
ctx.stroke();
```

![image-20221219153834935](C:\Users\dell\AppData\Roaming\Typora\typora-user-images\image-20221219153834935.png)

```js
如上图所示，先画的半圆弧和后画的圆弧被连在了一起，其实这是因为在咱们每次新建路径的时候都需要开启和闭合路径，这样不同路径之间才不会相互干扰。所以需要开启和闭合路径
```

