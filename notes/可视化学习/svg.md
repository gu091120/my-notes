# SVG 学习

## 使用

-   通过图像引用

```html
<img src="image.svg" alt="My SVG image" />
```

-   直接内嵌在 HTML

```html
<!DOCTYPE html>
<html>
    <head>
        <title>A page</title>
    </head>
    <body>
        <svg width="10" height="10">
            <rect x="0" y="0" width="10" height="10" fill="blue" />
        </svg>
    </body>
</html>
```
## 视口

### viewport、viewbox 、preserveAspectRatio
```html
<svg width="100"  height="100" viewbox="0,0,20,50" preserveAspectRatio="xMidYMid meet">
    <rect y="0" x="0" height="10" width="10" style="stroke:#333;fill:none" />
</svg>
```
画布视口：viewport

视图的窗口: viewbox 
    - 说明：相当于选择画布某个区域，进行展示，
    - 参数：[`原点x轴坐标`] [`原点Y轴坐标`] [`视口的宽度`] [`视口的高度`]

preserveAspectRatio：
    - 说明：设置viewbox和viewport对齐方式和如何维持高宽比
    - 参数：[`左右对齐` `上下对齐`] [`如何维持高宽比`]

| 值(左右对齐) | 含义 |  值（上下对齐） | 含义 |  值（上下对齐） | 含义 | 
| :-----:| :----: |  :-----:| :----: | :-----:| :----: | 
| xMin | 左边对齐|  YMin | 顶部对齐| meet | 保持纵横比缩放viewBox适应viewport，受| 
| xMid | 左右居中 | YMid | 上下居中 | slice | 保持纵横比同时比例小的方向放大填满viewport，攻 | 
| xMax | 右边对齐 | YMax | 底部对齐 | none | 扭曲纵横比以充分适应viewport，变态 | 



实践：放大缩小




## 常用标签

### 图形

-   circle: 创建一个圆
-   rect: 创建一个矩形
-   line: 创建一条线
-   path: 在两点之间创建一条路径
-   polygon: 允许创建任意类型的多边形


### 动画


### 文本
-   textPath: 在两点之间创建一条路径，并创建一个链接文本元素


## 坐标系改变


### transform 
- matrix(<a> <b> <c> <d> <e> <f>): 矩阵变换
- translate(<tx> [<ty>]):左右移动
- scale(<sx> [<sy>]): x轴缩放，y轴缩放，
- skewX,skewY:倾斜角度
-  rotate(<rotate-angle> [<cx> <cy>]): 旋转角度,默认是坐标系的圆心，通过，cx，cy来设置

