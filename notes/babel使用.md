
# babel 使用
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




