# preact实现原理

## 简单实现
https://codesandbox.io/s/wnzqpozl08◊

## jsx解析
通过babel plugins babel-plugin-transform-react-jsx 编译DOM结构


```
// in
var a = () => <div>hello world</div>


//out 
var a = () => React.createElement(
  "div",
  null,
  "hello world"
);

```
#### babel-plugin-transform-react-jsx
可以通过`pragme`设置自定义编译
```
"plugins": [
        ["transform-react-jsx", { "pragma":"h" }]
    ]
```



##  render()
render()就是react中的ReactDOM.render(vnode,parent,merge),将一个vnode转换成真实DOM,插入到parent中，只有一句话，重点在diff中


## diff
diff主要做三件事

- 调用idiff()生成真实DOM

- 挂载dom

- 在组件及所有子节点diff完成后，统一执行收集到的组件的componentDidMount()


#### idiff 

调用idiff()生成真实DOM










### Virtual Dom 