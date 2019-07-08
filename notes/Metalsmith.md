# Metalsmith 使用

## 主要功能

对导入模版资源作为一个数组排序，将内容转为buffer,调用插件对模版内容进行修改，配合 [`Handlebars`](https://handlebarsjs.com/)，完成模版配置输出。

## demo
```javascript
const Metalsmith = require("metalsmith")
const metalsmith = Metalsmith(templatePath)
 metalsmith
        .source("template") //设置template所在文件名称
        .metadata({
            name: project_name //给metadata设置数据
        })
        .destination(getDeskPath(project_name)) //输出文件设置地址
        .use(askQuestions(opts.prompts)) //自动插件使用
        .use(renderTemplate())
        .build(err => { //执行
            done(err)
        })
```

## 主要API

- source：设置template所在文件名称
- metadata：设置metadata设置数据
- destination：输出文件设置地址
- use:插件调用
    - 插件编写规范
    ```javascript
    function fn(){
        //files:导入模版资源对数组，metalsmith:metalsmith的引用，可以动态修改metalsmith的配置内容，done:异步完成动作
        return (files, metalsmith, done)=>{ 
            //可以动态的获取metalsmith对象中metadata的引用，可以获取值，也可以设置新的值
            let data = metalsmith.metadata() 
            files.forEach(file=>{
                //do something
            })
            done()
        }
    }
    ```
- ignore：忽略的文件
- clean：设置是否在写入之前删除目标目录（默认:true）


## Handlebars 使用

### 主要功能
对文件进行模版渲染

### demo
```javascript
const source = `<div>hello,{{name}},my age:{{age}}</div>`

const Handlebars = require("handlebars")

const template = Handlebars.compile(source)

const res = template({name:1,age:2})

```