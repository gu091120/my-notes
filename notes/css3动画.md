# css3 动画
## 基础概念
- 补间动画：自动完成从起始状态到终止状态的的过渡。不用管中间的状态。
- 帧动画：通过一帧一帧的画面按照固定顺序和速度播放。如电影胶片。

## transform
变化都是以`transform-origin:x,y`为中心（默认：对角线中心）

- 旋转(roate(30deg)):以对角线中心顺时针选装30度
![旋转](https://github.com/gu091120/my-notes/blob/master/static/css3%E5%8A%A8%E7%94%BB-1.png)
- 移动(translate(100px,20px)):整体向右平移100px,向下平移20px。
![移动](https://github.com/gu091120/my-notes/blob/master/static/css3%E5%8A%A8%E7%94%BB-2.png)
- 缩放(scale(2,1.5)):以对角线中心到水平方向左右各延长1倍，垂直方向延长0.5倍
![缩放](https://github.com/gu091120/my-notes/blob/master/static/css3%E5%8A%A8%E7%94%BB-3.png)
- 扭曲(skew(30deg,10deg)):垂直轴逆时针偏移30度，水平方向顺时针方向偏移10度
![扭曲](https://github.com/gu091120/my-notes/blob/master/static/css3%E5%8A%A8%E7%94%BB-4.png)
- 矩阵(matrix（a,b,c,d,e,f):以上的实现都是以这个矩阵为基础的
![矩阵](/static/css3%E5%8A%A8%E7%94%BB-5.png)

[详细参考:理解CSS3 transform中的Matrix(矩阵)](https://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/)


## transition：

控制补间动画的因素：

- 需要过度动画属性(transition-property):可以是全局属性（all）
- 过度持续时间(transition-duration):1s
- 时间和变化(transition-timing-function）:线性(linter)、减速（ease）、加速（ease-in）、减速（ease-out）、先加速后减速(ease-in-out)
- 延迟执行时间(transition-delay):过渡延迟。多长时间后再执行这个过渡动画。

## animation