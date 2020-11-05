# 数学理论相关

## 如何用向量和坐标系描述点和线段？

向量包含：

- 长度： `v.length = function(){return Math.hypot(this.x, this.y)};`（x、y 的平方和再开平方根）
- 方向：`v.dir = function() { return Math.atan2(this.y, this.x);}`（向量与 x 轴的夹角，取值范围是 -π 到 π，正数表示在 x 轴上方，负数表示在 x 轴下方）

根据长度和方向的定义可推导出：

```
v.x = v.length * Math.cos(v.dir);
v.y = v.length * Math.sin(v.dir);
```

## 可视化中需要掌握的向量乘法知识

> 参考：
>
> - [标量和向量的定义 - wiki](https://zh.wikipedia.org/wiki/%E6%A0%87%E9%87%8F)
> - [向量点乘（内积）和叉乘（外积、向量积）概念及几何意义解读 - CSDN](https://blog.csdn.net/dcrmg/article/details/52416832)

### 点乘

向量的点积：

- 几何意义：b 向量在 a 向量方向上的投影
- 物理意义：a 力作用于物体，产生 b 位移所做的功

公式：

![08ed8e6ded30ae53d8d3900e7f8bee36](math-related.assets/08ed8e6ded30ae53d8d3900e7f8bee36.jpg)

### 叉乘

向量的叉积：

- 几何意义：在三维几何中，向量 a 和向量 b 的叉乘结果是一个向量，更为熟知的叫法是法向量，该向量垂直于 a 和 b 向量构成的平面

![20160902232814429](math-related.assets/20160902232814429.jpg)

- 物理意义：力产生的力矩

公式：

![72227ffca461a60a1e79c0f54b6777ca](math-related.assets/72227ffca461a60a1e79c0f54b6777ca.jpg)

## 如何用向量和参数方程描述曲线？

圆的参数方程：圆心坐标 (x0,y0)，半径长度为 r，θ∈[0，2π)

![679bb841b70f7c7bae35d84c98a86b09](math-related.assets/679bb841b70f7c7bae35d84c98a86b09.jpeg)

```js
const TAU_SEGMENTS = 60; // 整圆由60个线段组成
const TAU = Math.PI * 2; // 一个整圆的弧度
function arc(x0, y0, radius, startAng = 0, endAng = Math.PI * 2) {
  const ang = Math.min(TAU, endAng - startAng); // 弧度为负数时好像有问题吧？endAng - startAng 再加个绝对值吧
  const ret = ang === TAU ? [] : [[x0, y0]];
  // 构成图形的弧线的段数 = 图形弧度(ang) / 整圆弧度(2PI) * 整圆弧线段数(TAU_SEGMENTS)
  const segments = Math.round(TAU_SEGMENTS * ang / TAU);
  for(let i = 0; i <= segments; i++) {
    const x = x0 + radius * Math.cos(startAng + ang * i / segments);
    const y = y0 + radius * Math.sin(startAng + ang * i / segments);
    ret.push([x, y]);
  }
  return ret;
}

draw(arc(0, 0, 100)); // 在 (0,0) 点绘制一个半径为 100 的圆
```

## 使用三角剖分填充多边形以及判断点是否在多边形内部

1. 填充任意多边形：Canvas2D 使用 ``ctx.fill()``；WebGL 使用成熟的库对多边形进行三角剖分（[Earcut](https://github.com/mapbox/earcut)、[Tess2.js](https://github.com/memononen/tess2.js)、[cdt2d](https://github.com/mikolalysenko/cdt2d)）。

2. 判断点是否在多边形内部：将图形进行三角剖分后，根据点与三角形的数学关系来判断点是否在某个三角形的内部或边上。



### 使用向量判断点是否在三角形内部或边上

已知一个三角形的三条边分别是向量 a、b、c，平面上一点 u 连接三角形三个顶点的向量分别为 u1、u2、u3，那么 u 点在三角形内部的 [充分必要条件](https://zh.wikipedia.org/wiki/%E5%85%85%E5%88%86%E5%BF%85%E8%A6%81%E6%9D%A1%E4%BB%B6) 是：u1 X a、u2 X b、u3 X c 的符号相同。

![3402b08454dbc39f9543cb4c597419c3](math-related.assets/3402b08454dbc39f9543cb4c597419c3.jpg)

[论证过程](https://time.geekbang.org/column/article/258101) 没看懂，需要再细看

## 如何用仿射变换对几何图形进行坐标变换？

[全篇](https://time.geekbang.org/column/article/259264) 都没看懂