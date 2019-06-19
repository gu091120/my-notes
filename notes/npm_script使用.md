# npm_script使用

## 原理

-   在执行npm script脚本的时候会新建一个 shell并且把`node_modules/.bin`加入到环境变量中，所以我们执行安装的包的时候并不需要指定文件目录

## 通配符

-   由于是`shell`命令所以可以使用 `**/*.js` 这样的通配符

## 传参

-   向 npm 脚本传入参数，要使用--标明。

```
npm run start -- --port 1010
```

## 执行顺序

-   并行

```
npm run start & npm run build
```

-   先后执行

```
npm run start && npm run build
```

## 钩子

-   在运行`npm run build`的时候它的执行顺序 `npm run prebuild` > `npm run build` > `npm run postbuild` 。所以我们可以在运行脚步的时候需要准备的动作放在`prebuild`, 而运行脚步后的处理放在 `postbuild` 中 ，如

```
{
    "script":{
        "prebuild":" rm -rf dist",
        "build":" webpack "
        "post":"echo build success"
    }
}
```

-   自定义`npm run myscript`那两个钩子分别是 `premyscript` 和`postmyscript`

-   npm 默认提供下面这些钩子。

```
prepublish，postpublish
preinstall，postinstall
preuninstall，postuninstall
preversion，postversion
pretest，posttest
prestop，poststop
prestart，poststart
prerestart，postrestart
```

## 变量使用

-   在script中,获取`webpack`中`config`的`port`

```
{
    script:{
        "myscript":"echo $npm_config_port"
    }
}
```

-   在node环境中

```
console.log(process.npm_config_port)
```

## 参考链接

[http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html](http://www.ruanyifeng.com/blog/2016/10/npm_scripts.html)


