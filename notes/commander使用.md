# commander 

## version

设置版本信息
```
.version("1.0.0")
```

## option

设置启动参数格式 `commander.options(参数,["端口号"],正则或者fn,"默认值")`

- 参数值为bool
```
.option("-s,--show","isShow?")
```

- 参数为需要输入的具体个值

```
.option("-n,--name<name>","name")
```

- 对输入的值进行设置,并且在设置默认值（在输入值不在限定范围中,而不是不需要输入）

```
.option("-n,--name<name>","name",/^(xiaoming|xiaohong)$/i,"xiaoming")

```

- 对输入的值进行处理,`val`(输入都值),`设置都默认值`(mon)

```
.option("-a--arr<arr>","arr",(val,mon)=>{
    mon.push(val)
    return mon
},[])
```
## command

可以自定义命令

```
.command("start <dir> [other...]","描述内容" )
.action((dir,other)=>{
    console.log(`dir %10s %10j`,dir,other)
})
```
