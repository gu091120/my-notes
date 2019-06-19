# css3 动画
## 基础概念
- 补间动画：自动完成从起始状态到终止状态的的过渡。不用管中间的状态。

- 帧动画：通过一帧一帧的画面按照固定顺序和速度播放。如电影胶片。

## transform
变化都是以`transform-origin:x,y`为中心（默认：对角线中心）

- 旋转(roate(30deg)):以对角线中心顺时针选装30度
![8c0891544e5a1507bb0f42f26b0cfb2f.png](evernotecid://2F3D3A54-2321-48AD-B3E9-9609C9FF951E/appyinxiangcom/17835618/ENResource/p56)

- 移动(translate(100px,20px)):整体向右平移100px,向下平移20px。
![672565bc47ceed7f88399fe5b16c9bae.png](evernotecid://2F3D3A54-2321-48AD-B3E9-9609C9FF951E/appyinxiangcom/17835618/ENResource/p57)

- 缩放(scale(2,1.5)):以对角线中心到水平方向左右各延长1倍，垂直方向延长0.5倍
![672565bc47ceed7f88399fe5b16c9bae.png](evernotecid://2F3D3A54-2321-48AD-B3E9-9609C9FF951E/appyinxiangcom/17835618/ENResource/p57)

- 矩阵(matrix（a,b,c,d,e,f）)
![a21da3258a26e7ff2b32661c7ae9dad1.gif]()

[详细参考:理解CSS3 transform中的Matrix(矩阵)](https://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/)


## transition：

控制补间动画的因素：

- 需要过度动画属性（transition-property）:可以是全局属性（all）
- 过度持续时间(transition-duration):1s
- 时间和变化（transition-timing-function）:线性(linter)、减速（ease）、加速（ease-in）、减速（ease-out）、先加速后减速(ease-in-out)
- 延迟执行时间(transition-delay) ：过渡延迟。多长时间后再执行这个过渡动画。

## animation