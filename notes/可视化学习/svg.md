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

