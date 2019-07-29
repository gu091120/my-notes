# babel 使用

## 转译过程

ES6 代码 => 解析代码生成 AST 语法树 (`parse`) => 遍历 AST 语法树，先调用 plugin，再用`presets`配置转译成`ES5` (`transform`) => 输出 ES5 (`generate`)

### 解析代码，生成 AST 语法树

这里主要用到了[`babel-parser`](https://github.com/babel/babel/tree/master/packages/babel-parser),是 babel 的解析器，将 javascript 解析成 AST 语法树， 默认只支持 `javascript` 的部分语法， 通过在 `presets` 设置：

-   @babel/preset-env :解析高级的 JavaScript 语法
-   @babel/preset-flow ：解析 flow 语法
-   @babel/preset-react ：解析 react
-   @babel/preset-typescript ：解析 typescript

```
var a = 11;
//AST 语法树
{
  "type": "Program",
  "start": 0,
  "end": 190,
  "body": [
    {
      "type": "VariableDeclaration",
      "start": 179,
      "end": 189,
      "declarations": [
        {
          "type": "VariableDeclarator",
          "start": 183,
          "end": 188,
          "id": {
            "type": "Identifier",
            "start": 183,
            "end": 184,
            "name": "a"
          },
          "init": {
            "type": "Literal",
            "start": 186,
            "end": 188,
            "value": 12,
            "raw": "12"
          }
        }
      ],
      "kind": "var"
    }
  ],
  "sourceType": "module"
}
```

### 遍历 AST 语法树，先调用 plugin，再用`presets`配置转译成`ES5`

#### 调用`plugin`

官方的许多 plugin 其实和 preset 有类似的功能，preset 将所有可能用到高级语法都注入，而像 `@babel/plugin-transform-arrow-functions` 这个 plugin 主要是针对箭头函数的，可以做到较少的引入，但是自定义的工作量就比较高。

多个 plugin 的执行顺序：从数组最后往前依次执行

> 拓展 [plugin 自定插件编写](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/plugin-handbook.md#toc-basics)

#### 用`presets`配置转译成`ES5`

通过 [`babel-core`](https://github.com/babel/babel/tree/master/packages/babel-core) 也只能将 ES6 部分转译成 ES5 的代码，也需要像解析时一样，在 `presets` 设置：

-   @babel/preset-N : 转译高级的 JavaScript 语法
-   @babel/preset-flow ：转译 flow 语法
-   @babel/preset-react ：转译 react
-   @babel/preset-typescript ：转译 typescript

### 输出 ES5 (`generate`)

最后将转译后 AST 语法树，通过[`@babel/generator`](https://github.com/babel/babel/tree/master/packages/babel-generator)输出为 ES5 的语法

## 转译的方案(babel v7)

-   将需要兼容的所有新的语法统一在入口文件引入(或者手动义引入特定的包):这个问题就是打包时会引入一些没有用的新的语法依赖。手动引入可以解决这个问题，但是需要维护这个引入包，多人开发时就会很容易出现问题。

效果

```
//in
import "@babel/polyfill";


//out
import "core-js/modules/es7.string.pad-start";
import "core-js/modules/es7.string.pad-end";
```

配置

```javascript
//.babelrc(babel 7)
{
  "preset":{
    [
      "@babel/preset-env"
      {
        "useBuiltIns":"entry"
      }
    ]
  }
}

//main.js(入口文件)
require("@babel/polyfill");

//do some

```

-   自动引入模块所用的新语法的资源（bable 7）: 这个方案解决上面两个方案的问题。
    效果

```
//in
//a.js
var a = new Promise();

//b.js
var b = new Map();

//out
//a.js
import "core-js/modules/es6.promise";
var a = new Promise();

//b.js
import "core-js/modules/es6.map";
var b = new Map();

```

配置

```json
//.babelrc(babel 7)
{
  "preset":{
    [
      "@babel/preset-env"
      {
        "useBuiltIns":"usage",
        "corejs": 2, //需要单独单独引入 @babel/runtime-corejs2
      }
    ]
  }
}

```

## 优化

-   使用 `plugin-transform-runtime` : 在上面哪些方案中，对于新的 API,比如`Array.from`,都是在 `Array.prototype.from` 进行拓展，所以会存在污染全局环境的问题。而`bable-runtime`解决了这个问题，将这些对于全局进行隔离。


```javascript
// 输入的ES6代码
var sym = Symbol();
// 通过transform-runtime转换后的ES5+runtime代码
var _symbol = require("babel-runtime/core-js/symbol");
var sym = (0, _symbol.default)();
```






## `polyfill` 和 `core-js`

babel默认只能将部分语法转译，像 Set ，Met等语法并不会转译，babel,通过 `polyfill` 为整个环境提供一个兼容（shim），而`polyfill`实际只是对 `core-js`的封装。对于`core-js`,使用有二种模式：
-  全局引用：这个也就是我们编译方案的第一种
```javascript
require("core-js")
var a = Set Map()
```

-  引用部分：只针对需要的部分引入

```javascript
var Set = require('core-js/library/fn/set');
var a = Set Map()

```






##

## 配置文件

.babelrc 文件配置

```json
{
    "presets": [
        [
            "@babel/preset-env",
            {
                "targets": //指定目标环境
                    {
                        //指定支持的版本
                        "browsers":["last 2 versions","iOS >= 8","Android >= 4"],
                        "node":"9.8" //或者 "node":"current"//以当前运行环境为目标进行编译
                    },
                 "loose": false,//是否不用严格模式(默认true)
                "modules": false,//是否将代码转成统一模块输出标准（"amd" | "umd" | "systemjs" | "commonjs" | "cjs" | "auto" | false）默认default
                // "corejs": 2,
                // "useBuiltIns": "entry"

            }
        ],
        "react",
        "stage-0"
    ],
    "plugins": [
        "@babel/plugin-transform-runtime",

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

### babel-cli

```shell
babel a.js -o a-compiled.js  //-o 指定输出文件
babel src -d dist //-的 指定文件夹
babel src -d dist --ignore a.js src //忽略的文件/文件夹
babel a.js -o a-complied.js  -s 生成source-map 文件
```

[bable 中文手册](https://github.com/jamiebuilds/babel-handbook/blob/master/translations/zh-Hans/user-handbook.md)
