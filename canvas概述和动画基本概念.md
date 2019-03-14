canvas 元素是 HTML5 中新出现的，我们可以将其当做一个像素级的画布，它

允许我们绘制直线、圆、矩形等基本形状，以及图像和文字。使用 canvas 元素，
可以实时渲染图形、游戏动画或其他虚拟图像

，而且它已经为快速绘图做过优化了。各大主流浏览器都已经支持 GPU 加速的 2D canvas 渲染，因此，使用 canvas 绘制出的游戏动画运行速度会很快。

兼容性：

在《canvas 动画包教不包会》系列，我们主要是使用 HTML5 canvas 和 JavaScript 技术。如果你对这两 canvas 和 JavaScript 还很陌生，建议先去了解熟悉一下，你可以看我的文章来了解：《canvas 入门基础系列》和《JavaScript 学习笔记》，也可以到《HTML5 Canvas》和《JavaScript 教程》，当然，还有很多优秀的书籍、文章和教程，自主选择学习！

# 一、canvas
在 canvas 上绘制动画的基本文档结构：

<!DOCTYPE html>

<html lang="en">

<head>

  <meta charset="UTF-8">

  <title></title>

</head>

<body>

  <canvas id="canvas" width="400" height="500">

    <P>你的浏览器不支持“canvas”！</P>

  </canvas>

  <script>   

    window.onload = function(){   

      var canvas = document.getElementById('canvas');  // 获取canvas元素

      var ctx = canvas.getContext('2d');  // 获取'2d'context对象

      // 绘画代码

    }; 

  </script>

</body>

</html>

下面简要的罗列一下 canvas API：
rect( x, y, width, height ) 绘制矩形

fillRect( x, y, width, height ) 绘制被填充的矩形

strokeRect( x, y, width, height ) 绘制矩形（无填充）

clearRect( x, y, width, height ) 清除指定的矩形内的像素

fill() 填充当前绘图（路径）

stroke() 绘制已定义的路径

beginPath() 起始（重置）当前路径

moveTo( x, y ) 将笔触移动到指定的坐标(x,y)

lineTo( x, y ) 绘制一条从当前位置到指定的坐标(x,y)的直线

clip() 从原始画布剪切任意形状和尺寸的区域

quadraticCurveTo() 创建二次贝塞尔曲线

bezierCurveTo() 创建三次贝塞尔曲线

arc( x, y, radius, startAngle, endAngle, anticlockwise) 绘制圆或圆弧

arcTo( x1, y1, x2, y2, radius) 根据给定点画圆弧，再以直线连接两个点

isPointInPath( x, y ) 检测指定的点是否在当前路径中，在则返回 true。

fillStyle 设置或返回用于填充绘画的颜色、渐变或模式

strokeStyle 设置或返回用于笔触的颜色、渐变或模式

shadowColor 设置或返回用于阴影的颜色

shadowBlur 设置或返回用于阴影的模糊级别

shadowOffsetX 设置或返回阴影与形状的水平距离

shadowOffsetY 设置或返回阴影与形状的垂直距离

lineCap 设置或返回线条的结束点样式（butt、round、square）

lineJoin 设置或返回当两条线交汇时，边角的类型（bevel、round、miter）

lineWidth 设置或返回当前的线条宽度

miterLimit 设置或返回最大斜接长度

createLinearGradient( x0, y0, x1, y1 ) 创建线性渐变

createPattern( image/canvas/video, repeat ) 在指定的方向内重复绘制指定的元素

createRadialGradient( x0, y0, r0, x1, y1, r1 ) 创建径向渐变

addColorStop( stop, color ) 规定渐变对象中的颜色和停止位置

font 设置或返回文本内容的当前字体属性（和 css 的 font 一样）

textAlign 设置或返回文本内容的当前对齐方式

textBaseline 设置或返回在绘制文本时使用的当前文本基线

fillText( text, x, y ) 在画布上绘制“被填充”的文本

strokeText( text, x, y ) 在画布上绘制文本（无填充）

measureText( text ) 返回包含指定文本宽度的对象（属性 width 获取宽度）

drawImage( image/canvas, x, y )、drawImage( image/canvas, x, y, width, height )、drawImage( image/canvas, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight ) 在画布上绘制图像、画布或视频

createImageData( width, height )、createImageData(imageData) 绘制 ImageData 对象

getImageData( x, y, width, height ) 返回 ImageData 对象，该对象为画布上指定的矩形复制像素数据。

putImageData( ImageData, x, y )、putImageData( imageData, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight ) 把图像数据放回画布上。

width 返回 ImageData 对象的宽度

height 返回 ImageData 对象的高度

data 返回一个对象，包含指定的 ImageData 对象的图像数据

globalAlpha 设置或返回绘图的当前 alpha 或透明度

globalCompositeOperation 设置或返回新图像如何绘制到已有的图像上。

scale( x, y ) 缩放当前绘图

translate( x, y ) 重新设置画布上的(0,0)位置

rotate( angle ) 选择当前绘图，单位为“弧度”，角度转弧度公式（ degrees\*Math.PI/180）

transform( m11, m12, m21, m22, dx, dy ) 替换绘图的当前转换矩阵

setTransform() 将当前转换重置为单元矩阵，然后运行 transform()

save() 保存当前环境的状态

restore() 恢复之前保存过的路径状态和属性

getContext('2d') 获取 2d 对象

toDataURL() 将 canvas 转换成图片，返回地址

只要你熟练的使用上面这些 canvas API，你就能实现很多酷炫的动画。

# 二、动画（animation）的基础概念

动画，其实是一个创造运动假象的过程，通俗讲就是，动画是由一幅幅不同的静态画面以极快的速度连续播放从而产生物体运动或变化。由于快速频率，我们的眼睛就会欺骗我们的大脑，也就是前面说的运动假象。

每一幅静态画面我们称做一“帧”。（gif 图的原理就一帧一帧的存储，然后播放）

上面是动画的基础概念，那如何在 canvas 上产生动画呢？

首先，我们要知道实现动画的步骤，一般分为四步：
清空 canvas（使用 clearRect()或全图绘制）
保存 canvas 状态（可选）
绘制动画图形
恢复 canvas 状态（一般在第二步的基础上使用）

在了解绘制步骤后，我还需要了解三种用来绘制动画的方法：

（1）使用时间控制器
setInterval( function, delay )

setTimeout( function, delay )

具体用法在这里就不多说了，不熟悉的请先去学习一下 JavaScript，不是看不起你，而是没 JavaScript 基础，是很难开发动画的。

（2）循环本身
window.requestAnimationFrame( function )

requestAnimationFrame()是一个新的 API，和 setInterval 差不多，但是使用 requestAnimationFrame()，你必须主动采用循环调用自身。

requestAnimationFrame()不需要设置时间，它会根据浏览器的刷新频率自动调整动画的时间间隔，一般只有十几毫秒，可用它来做逐帧动画。
window.requestAnimationFrame = (function() {

return window.requestAnimationFrame || window.webkitRequestAnimationFrame || window.mozRequestAnimationFrame || function(callback) {

    window.setTimeout(callback, 1000 / 60);

};

})();

还有个停止 requestAnimationFrame()动画的方法 cancelAnimationFrame(ID)，参数 ID 是调用 requestAnimationFrame()返回来的 ID 值：
window.cancelAnimationFrame = (window.cancelRequestAnimationFrame || window.webkitCancelAnimationFrame || window.webkitCancelRequestAnimationFrame || window.mozCancelAnimationFrame || window.mozCancelRequestAnimationFrame || window.msCancelAnimationFrame || window.msCancelRequestAnimationFrame || window.oCancelAnimationFrame || window.oCancelRequestAnimationFrame || window.clearTimeout);

像我的个人主页上的粒子效果就是用 requestAnimationFrame()方法来实现的，我也单独做了一个粒子效果页面：粒子效果

总结
要实现动画，一定要熟练的使用 canvas API 和对 JavaScript 有一定的了解。
动画的实质就是由一幅幅不同的静态画面以极快的速度连续播放从而产生物体运动或变化。
# 了解更多https://www.w3cschool.cn/xjmuw/xjmuw-km4925xb.html

# 微信小程序画布 canvas https://www.w3cschool.cn/weixinapp/weixinapp-canvas.html