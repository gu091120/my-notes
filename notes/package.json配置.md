# package.json 配置


## 常用配置解释

```
{
    "name": "project_name",  //包的名称。注意：不能有大写字母以及 "."和 "_"开头
    "version": "1.0.0", //版本号
    "description": "a simple description for help people to use  ", //包的介绍
    "main": "dist/index.js", //指定了模块的入口程序文件
    "bin":"dist/index.js", //全局配置的指定，它是一个命令名和本地文件名的映射
    "config": { //添加一些设置，可以供scripts读取用，同时这里的值也会被添加到系统的环境变量中
        "port": "8080"
    },
    "keywords": [ //包的关键词信息，是一个字符串数组，同上也将显示在npm search的结果中
        "react",
        "redux",
        "react-redux"
    ],
    "author": "author_name", //作者 -- 注:1
    "license": "ISC", //使用权利和和任何限制
    "scripts": { //scripts字段是一个由脚本命令组成的字典
        "build": "babel src -的 dist "
    },
    "files":["a.js","b.js"], //files字段是一个被项目包含的文件名数组
    "directories":{ //CommonJS包所要求的目录结构信息，展示项目的目录结构信息。字段可以是：lib, bin, man, doc, example。值都是字符串
        "lib":"lib",
        "docs":"docs"
    },

    "repository": { //包的仓库地址
        "type": "git",
        "url": "https://github.com/project"
    },
    "homepage":{ //包的主页地址
        "url": "https://github.com/project"
    },
    "devDependencies": { //这些依赖只有在开发时候才需要 -- 注:2
        "babel-preset-env": "^1.7.0",
        "babel-preset-react": "^6.24.1",
        "babel-preset-stage-0": "^6.24.1"
    },
    "dependencies":{ //指定依赖的其它包，这些依赖是指包发布后正常执行时所需要的
        "react": "^16.4.2"
    },
    "peerDependencies":{ //相关的依赖，如果你的包是插件，而用户在使用你的包时候，通常也会需要这些依赖（插件），那么可以将依赖列到这里
        "react": ">=15.0.0",
        "react-dom": ">=15.0.0",
    },
    "bugs": { //改进项目的issue跟踪页面或这报告issue的email地址
        "url": "https://github.com/project/iussus",
        "e_mail":"youremailaddress@qq.com"
    },
    "engines":{ //指定项目运行环境
        "node" : ">=0.10.3 <0.12"
        "npm":">=0.1.2<0.13"
    },
    "preferGlobal":true ,//是否默认全局安装
    "os" : [ "darwin", "linux" ], //指定操作系统 也可以黑名单 : "os" : [ "!win32" ]
    "cpu" : [ "x64", "ia32" ]， //指定处理器 也可以是黑名单
}
```

-   注:1 ---- author 是一个人，contributors 是一些人的数组。person 是一个对象，拥有必须的 name 字段和可选的 url 和 email 字段, 如

```
{
    "name": "Barney Rubble",
    "email": "b@rubble.com",
    "url": "http://barnyrubble.tumblr.com/"
}
```

-   注:2 ---- dependencies 属性是一个对象，配置模块依赖的模块列表，key 是模块名称，value 是版本范围，版本范围是一个字符，可以被一个或多个空格分割。
    dependencies 也可以被指定为一个 git 地址或者一个压缩包地址。

```
{
    "dependencies" :{
        "foo" : "1.0.0 - 2.9999.9999"
        , "bar" : ">=1.0.2 <2.1.2"
        , "baz" : ">1.0.2 <=2.3.4"
        , "boo" : "2.0.1"
        , "qux" : "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0"
        , "asd" : "http://asdf.com/asdf.tar.gz"
        , "asdd" : "git://github.com/user/project.git#commit-ish"
        , "til" : "~1.2"
        , "elf" : "~1.2.3"
        , "two" : "2.x"
        , "thr" : "3.3.x"
        , "lat" : "latest"
        , "dyl" : "file:../dyl"
    }
}
//Git URLs as Dependencies

git://github.com/user/project.git#commit-ish
git+ssh://user@hostname:project.git#commit-ish
git+ssh://user@hostname/project.git#commit-ish
git+http://user@hostname/project/blah.git#commit-ish
git+https://user@hostname/project/blah.git#commit-ish

//Local Paths

{
    "bar": "file:../foo/bar"
}
```

[更多配置说明](https://www.cnblogs.com/tzyy/p/5193811.html)

## 参考文档列表

[https://docs.npmjs.com/files/package.json#directorieslib](https://docs.npmjs.com/files/package.json#directorieslib)


