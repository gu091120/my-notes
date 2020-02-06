# Flex 布局
## 基本概念

 ![2c3e5aecdee4d9ddc9f63c6bc29221eb.jpeg](/notes/CSS/Flex布局/static/Flex布局-1.png)
 flxe布局是一个二维布局，所以主要分两个方向进行布局
 
 - 主轴：元素排列方向（默认是水平从左->右）
 - 交叉轴：与主轴垂直关系的

## 设置容器
 ### 1. 设置容器为Flex布局
`.box:{display:flex}`
 ### 2. 设置容器主轴方向（flex-direction）

![22730e06dfb5bd38f25ce7211d1cd829.gif](/notes/CSS/Flex布局/static/Flex布局-2.gif)

 - 左->右(row:默认)
 - 右->左(row-reverse)
 - 上->下(column)
 - 下->上(column-reverse)
 
 ### 3. 设置主轴对齐方式（justify-content）

 ![d410ef368eb769223fd04f7e9fdceb86.jpeg](/notes/CSS/Flex布局/static/Flex布局-3.png)
 
- flex-start
- flex-end
- center
- space-between
- space-around

#### 4. 设置交叉轴的对齐方式(algin-item/algin-content)
由于交叉轴的设置 `flex-warp`会有两种情况：

- 单行模式(nowarp):设置每行的状态，就算换行，也会将换行的这一行作为单独个体设置

![dcd7da4e33b13a901a88848fad3a8792.jpeg](/notes/CSS/Flex布局/static/Flex布局-4.png)
(algin-item:top)

- 多行模式(warp):将多行看成一个整体，就好比，justify-content,差不多；

![63e2035dd8c928359c5d75299c7b0409.jpeg](/notes/CSS/Flex布局/static/Flex布局-5.png)
(algin-content:top)

> ⚠️注意：`algin-content`只有在 `flex-warp:warp`才能生效果。
#### 单行模式(algin-item)

- stretch （如果item没有设置高度，默认）
- flex-start (如果item设置了高度，默认）
- flex-end
- flex-center
- baseline

 ![0ec9e81c35c66f66b23e724c6063fce8.png](/notes/CSS/Flex布局/static/Flex布局-6.png)



#### 多行模式(algin-content)
比单行模式多了两种情况，少了一种`baseline`

- space-bettwen
- space-around

![aade7abc9eb8c177c66d0128b1cc6ca9.png](/notes/CSS/Flex布局/static/Flex布局-7.png)


## item 设置
### 设置元素伸缩比
- 缩小比（flex-shrink）默认是 `1`：在元素总宽度大于容器宽度，就会自动所以元素宽度

![e24a8660e626cd488ee1e21645a92bb0.jpeg](/notes/CSS/Flex布局/static/Flex布局-8.png)
如果所有的项目的flex-shrink属性都为1，则空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性值为0，其它项目都为1，则空间不足时前者不缩小。
- 放大比（flex-grow）模式是 `0` ：默认当元素宽度小于容器宽度，元素不会自动填充满整个容器，只有元素设置`flex-grow`不为0的时候才会自动按比例填充容器.
- 基础比例（flex-basis），默认是auto：和直接设置宽度差不多作用



### 设置元素排列顺序（order）
- 数值越小，越靠主轴方向前，默认为0
- 值相同时，以dom中元素排列为准


### 设置单个元素交叉轴方向（align-self）
- flex-start
- flex-end
- center
- baseline
- stretch
- auto
 
![0d93c40b34a77529f71ddd927dd49c82.png](/notes/CSS/Flex布局/static/Flex布局-9.png)
   
