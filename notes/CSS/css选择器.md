# css 选择器

### 简单选择器

-   类型选择器：`p{color:red}`
-   id 选择器: `#idname{color:red}`
-   class 选择器`.className{color:red}`

### 伪元素

-   `::before`
-   `::after`

#### 文本

-   `::first-letter`:文本的第一个字符串
-   `::first-line`:文本的第一段

> 使用伪元素不能添加对内容有实质的影响
> 伪元素使用双冒号，而伪类是单冒号（一般现在浏览器都兼容）

### 伪类

-   `:hover`：鼠标 hover
-   `:active`：选中
-   `:focus`：聚焦
-   `:link`：链接
-   `:visited`：访问过了
-   `:target`: 浏览器的 hash 值为目标 ID

    ```html
    <!--  url:www.example.com#commit -->
    <style>
        .message:target {
            color: red;
        }
    </style>

    <!-- 显示的文字就会变成红色 -->
    <p class="message" id="commit">message</p>
    ```

-   `:not()`:反选
-   `div:first-child`:div 类型第一个元素
-   `div:last-child`：div 类型最后一个元素
-   `:first-of-type`:任意第一个子元素
-   `:last-of-type`: 任意最后一个元素

（css3 新增）

-   `div:nth-child(2n)`:div 类型匹配 2、4....偶数（可以用 odd 代替）
-   `div:nth-last-child(2n)`：类似第一个，但是从最后开始
-   `:nth-of-type(N)`:任意子节点的 N 个
-   `:nth-last-of-type(N)`:类似第一个，但是从最后开始

> 伪类和伪元素的区别，伪类：更方便的类型选择器；伪元素: 创建一个不存在于文档的容器（元素）

### 子代选择器

-   `空格`:全部后代
-   `>`:最近子代

### 兄弟选择器

-   `+`:相邻最近下一个兄弟
-   `~`:所有兄弟

### 属性选择器

-   `[href]`:选择带有该属性元素
    ```
    可以用一些匹配规则:
    a[href^="https://wwww.baidu.com"]:开始
    img[href$=".jpg"]：结束
    a[href*="/about/"]：包含
    a[rel~="next"]:匹配属性是多个以空格分开的值的其中一个
    a[lang|="en"]:可以匹配带斜杠的值（en,en-us）
    ```


### 优先级运算

第一优先：

-   `无连接符号`

第二优先级：

-   `空格`
-   `~`
-   `+`
-   `>`
-   `||`

第三优先级：

-   `,`
