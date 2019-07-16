
# babel 使用

## 转译过程

ES6 代码 => 解析代码生成AST语法树(parse) => 遍历AST语法树，转译成ES5(transform) => 输出 ES5(generate)

### 解析代码，生成AST语法树

这里主要用到了(`babel-parser`)[https://github.com/babel/babel/tree/master/packages/babel-parser],是babel 的解析器，将javascript 解析成 AST 语法树， 默认只支持 `javascript` 的部分语法， 通过在 `presets` 设置：

- @babel/preset-env :解析高级的JavaScript语法
- @babel/preset-flow ：解析 flow 语法
- @babel/preset-react ：解析 react
- @babel/preset-typescript ：解析 typescript 

### 遍历AST语法树，转译成ES5
#### 转译成ES5
通过 (`babel-core`)[https://github.com/babel/babel/tree/master/packages/babel-core] 也只能将 ES6 部分转译成 ES5的代码，也需要像解析时一样，在 `presets` 设置：

- @babel/preset-env : 转译高级的JavaScript语法
- @babel/preset-flow ：转译 flow 语法
- @babel/preset-react ：转译 react
- @babel/preset-typescript ：转译 typescript 

### 调用plugin










## 配置文件
 .babelrc 文件配置

```
{
    "presets": [
        [
            "env",
            {
                "targets":
                    {
                        //指定支持的版本
                        "browsers":["last 2 versions","iOS >= 8","Android >= 4"],
                        "node":"9.8" / "node":"current"//以当前运行环境为目标进行编译
                    }

            }
        ],
        "react",
        "stage-0"
    ],
    "plugins": [
        "transform-runtime",
        "transform-react-jsx"
    ],
    "env":{
        "devlopment":{
            "presets":[],
            "plugins":[]
        },
        "production":{
            "presets":[],
            "plugins":[]
        }
    }
}
```

#### 常用的插件

-   transform-remove-console ：移除 console.\*
-   transform-decorators-legacy ： 使用装饰器语法
-   transform-react-jsx: 对 .jsx 文件处理

### babel-cli

```
babel a.js -o a-compiled.js  //-o 指定输出文件
babel src -d dist //-的 指定文件夹
babel src -d dist --ignore a.js src //忽略的文件/文件夹
babel a.js -o a-complied.js  -s 生成source-map 文件
```

[bable 中文手册](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/user-handbook.md)




