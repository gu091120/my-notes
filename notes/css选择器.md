# css 选择器
## 简单选择器
- 类型选择器：`p{color:red}`
- 全体选择器: `*{color:red}`
- id选择器: `#idname{color:red}`
- class选择器`.className{color:red}`
- 属性选择器:`p[att=11]{color:red}`
- 伪类选择器:`p:before{color:red}`

## 选择器分组
- `空格`:全部后代
- `>`:最近子代
- `+`:相邻最近下一个兄弟
- `~`:所有兄弟
- `:first-child`：第一个子元素
- `:last-child`:最后一个子元素
- `:nth-child(n)`:子代选择第n个(n可以是公式)
    - `p:nth-child(2)`:第二个子元素
    - `p:nth-child(odd/even)`:所以奇数/偶数子节点
    - `P:nth-child(3n+0)`:所有3的倍数子节点
- `:nth-last-child(n)`:倒数子节点    
- `:not()`:选择除此之外的元素,`p:not(.other)`


## 优先级运算
第一优先：
- `无连接符号`

第二优先级：
- `空格`
- `~`
- `+`
- `>`
- `||`

第三优先级：
- `,`

