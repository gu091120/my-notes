# node readline
### 用途
- 逐行地读取文件流
- 命令行的交换

### Interface 类
通过 `readline.createInterface(options)`来生成实例

```
var rl = readline.createInterface({
    input:process.stdin,
    output:process.stdout
})
```

#### readline.createInterface(options)
- options <Object>
    - input <Stream.Readable>
    - output <Stream.Writeable>
    - completer <Function>  一个可选的函数，用于 Tab 自动补全
    - historySize <Number> 保留的历史行数的最大数量
    - prompt <String> 要使用的提示符，默认是 ">"
    - crlDelay <Number>  如果`\n`和`\r`自建的延迟超过crlDelay这个值，则 `\n` 和`\r`都会被当初换行符，默认值是100毫秒
    - removeHistoryDuplicates <Boolean> 如果为 true, 当新输入行与历史列表中的某行相同时， 那么移除旧有的行。 默认为 false
- return <Interface>







    


