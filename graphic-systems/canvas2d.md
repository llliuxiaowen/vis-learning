使用 canvas 绘制简单图形的过程：

1. 获取 Canvas 对象，通过 `getContext('2d')` 得到 2D 上下文；

2. 设置绘图状态，比如填充颜色 fillStyle，平移变换 translate 等等；

3. 调用 beginPath 指令开始绘制图形；

4. 调用绘图指令，比如 rect，表示绘制矩形；

5. 调用 fill 指令，将绘制内容真正输出到画布上。

   

详细教程和 api 参考 [Canvas 教程 - MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial)

