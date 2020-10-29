在 Web 上，图形通常是通过浏览器绘制的。现代浏览器是一个复杂的系统，其中负责绘制图形的部分是渲染引擎。渲染引擎绘制图形的方式大体上有 4 种：

|          | 优点                                                         | 不足                                                         | 用处                   |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------------------- |
| HTML+CSS | 不需要第三方依赖                                             | （1）CSS 属性不能直观体现数据，需要手工计算；（2）复杂图形会导致 HTML 元素多，消耗性能 | 绘制少量的、常见的图表 |
| SVG      | （1）绘制不规则图形；（2）通过属性设置图形，可以直观地体现数据 | 复杂图形会导致 SVG 元素多，消耗性能                          |                        |
| Canvas2D | （1）高性能绘制，直接操作绘图上下文；（2）使用简单           | （1）绘制的图形过多，或者处理大量的像素计算时，会有性能瓶颈；（2）不方便直接操作图形元素 |                        |
| WebGL    | （1）功能强大，能够充分利用 GPU 并行计算的能力进行大批量绘制；（2）内置了对 3D 物体的投影、深度检测等处理，适合绘制 3D 场景 | 使用复杂                                                     | 3D、大批量绘制         |
