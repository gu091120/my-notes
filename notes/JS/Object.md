# Object

### Object.defineProperty 定义对象属性

```javascript
var xiaoming={}

Object.defineProperty(xiaoming,"name",{
    value:"xiaoming",
    writable:true, // 是否可修改
    enumerable:false, // 是否可枚举
    configurable:true // 属性是否可以被修改
})

```