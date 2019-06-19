# 浏览器节点常用api

## 节点

### 节点类型

- Element:元素型
    - HTMLElement
    - SVGElement
- Document:文档根节点
- CharacterData:字符数据
- DocumentFragment:文档片段
    - Text:文本节点
    - Comment:注释
    - ProcessiongInstruction:处理信息
- DocumentType:文档类型

### 节点操作api
查找

- parentNode
- childNodes
- firstChild
- lastChild
- nextSibling
- previousSibling

修改

- appendChild
- insertBefore
- removeChild
- replaceChild

## Element
### 查找元素
- querySelector
- querySeletcorAll
- getElementById
- getElementsByTagName
- getElementsByClassName
 
`注意点：` 通过getElementSByTagName等方法获取的集合并非数组，而是一个能够动态更新的集合


## Attribute 

- getAttribute
- setAttribute
- removeAttribute
- hasAttribute




