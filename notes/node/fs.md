# Node-fs

fs对文件和文件夹都提供了两种操作模式：异步（回调），同步（sync）

### 文件路径
#### 可选类型
- `String`:字符串会被解析成绝对地址，或者相对地址。相对地址会按 `process.cwd()`定义为当前路径进行处理。支持 `file:`协议的`url`

- `Buffer`:用于在特定的 POSIX 系统上，将路径处理成 opaque 字节序列。 单一路径中可能包含多种字符编码的子序列。 Buffer 路径也可以是相对的或绝对的（并不理解...-.-）

- `fd`:文件描述符是node为打开的文件，抽象不同操作系统的差异，提供了统一的文件描述的数值标识。`fs.open()`用于分配一个新的文件描述符，一旦分配了可用于文件的读写。

### 文件的属性
`fs.Stats`提供了文件的属性，从`fs.stat()、fs.lstat()、fstat()`以及同步方法返回都是这个类型，如果`option`中的`bigint`为true，这返回的`bigint`类型
```
 var fs = require("fs")
 fs.open('/text.txt',(err,fd)=>{
    if(err) throw new Error(err)
    fs.stat(fd,stat=>{
        console.log(stat)
    })
    fs.close(fd)
 })
 
```
必须用`fs.close()`来关闭描述符

node版本`v10`版本提供了`fs.Dirent`有着和`fs.Stat`类似的方法。在`fs.readdir()`中`options`中`withFileTypes`设为`ture`就会返回一个`fs.Dirent`的数组

### 标识位flag
标识位代代表着对文件的操作方式，可读，可写，可读写
- `r`:可读，文件不存在则报错
- `w`:可写，如果文件不存在则新建
- `x`:新建，如果文件已经存在则会报错
- `a`:追加写入，不存在文件则新建
- `+`:可读可写（需要配合前面几个组合）

[详细说明](http://nodejs.cn/api/fs.html#fs_file_system_flags)

```
fs.open(path,"r+",(err,fd)=>{
    if (err) throw err;
        fs.writeFile(fd,"helloworld","utf-8",(err)=>{
            if (err) throw err;
            fs.readFile(fd,(err,data) =>{
                console.log(data) //打印:helloworld
            })
        })
})

```
表示打开的文件可以读写操作。但是如果在标识符为`r`去写入文件的时候就会报错。

### 文件夹操作

#### fs.readdir(path,[,options],callback) 读取目录内容
`callbanck(err,files)` ,`files`是目录中的文件名称的数组

- `options` : <String> | <Object>
    - endcoding: <String> 默认是`utf-8` 
    - withFileTypes: <Boolean> 默认是`false`
 
- `callback` : <Function> 
    - err <Error>
    - files <String [ ] >| <Buffer [ ]>| <fs.Dirent [ ]>
 如果  `endcoding`设为`buffer`,则返回的文件名称是个`buffer`。如果`withFileTypes`设为`true`则返回的文件名称是`fs.Dirent`(这个需要在node版本10以上)

#### fs.mkdir(path) 创建目录

- `path` <string> | <Buffer> | <URL>
- `ptions` <Object> | <integer>
    - `recursive` <boolean> 判断是否不是创建父目录，默认为 false
    - `mode` <integer> 不支持 Windows 平台。默认为 0o777。
- `callback` <Function>
    - `err` <Error>

#### fs.rmdir(path, callback) 删除目录
- `path` <string> | <Buffer> | <URL>
- `callback` <Function>
    - `err` <Error>

只能删除目录   



### 文件操作
#### fs.readFile(path，[,options,callback]) 读取文件

- `option`: <String> | <Object>
    - `encoding`:<String> | <null>默认是null
    - `flag`: <String> 默认`r`
- `callback` <Function>
    - `err`:<Error>
    - `data`:<String>
    
```
fs.readFile(path,"utf8",(err,data)=>{
    if(err) throw err
    console.log(data)
})
```

由于readfile会将整个文件放入内存，所以对大文件建议采用`fs.createReadFile()`形式来读取

如果`path`时目录的时候，一般操作系统会报错

#### fs.writeFile(path,data[,options,callback]) 清空写入/或者新建写入
- `data`: <String> | <Buffer> | <TypedArray> | <DataView>
- `option`: <String> | <Object>
    - `encoding`:<String> | <null>默认是null
    - `flag`: <String> 默认`r`
    - `mode`: <Integer> 默认为 0o666。
- `callback` <Function>
    - `err`:<Error>

如果文件不存在，则新建，存在则清空文件内容再写入,多次回调写入且不在回调函数中操作是不安全的，推荐使用`fs.createWriteStream()`
```
fs.writeFile(path,"helloworld","utf8",callback)

```
如果`data`是个`buffer`,则忽略`encoding`


#### fs.appendFile(path,data[,options,callback]) 追加写入

如果文件存在不会清空，而是追加写入。其他使用和`fs.writeFile`使用类似

#### fs.unlink(path,callback) 删除文件
删除文件，不支持删除目录,并且`path`不支持 `fd`(文件描述符)

#### fs.copyFile(src, dest[, flags], callback) 复制文件

- `src` <string> | <Buffer> | <URL> 拷贝的来源文件名。
- `dest` <string> | <Buffer> | <URL> 拷贝的目标文件名。
    - `flags` <number> 拷贝操作的修饰符。默认为 0。
- `callback` <Function>

如果目录不存在就会报错

#### fs.watchFile(path[, options], listener) 监视文件
当被监视文件有变动时会触发回调函数,只能监视文件，不支持目录

- `path`: <string> | <Buffer> | <URL>
- `option`:  <Object>
    - `persistent `:<Boolean> 默认是`true`，监视进程是否继续运行
    - `interval`: <Integer> 默认`5007`,轮询间隔时间
- `listener` <Function>
    - `current`:<fs.Stats> 当前文档信息
    - `previous`:<fs.Stats> 旧文档信息
```
fs.watchFile('文件.text', (curr, prev) => {
  console.log(`当前的最近修改时间是: ${curr.mtime}`);
  console.log(`之前的最近修改时间是: ${prev.mtime}`);
});
```

由于采用的事轮询机制，所以如果监视大量文件可能会造成内存溢出。推荐使用`fs.watch()`

#### fs.unwatchFile(path,listener) 移除触监听器
如果不指定`listener`就会移除所有触监听器



#### fs.watch(path[, options][, listener])

是`Even`的实现类，使用的是事件机制，所以性能上比`watchFile`好很多

- `path`: <String> | <Buffer> | <URL>
- `option`:  <Object> |<String>
    - `persistent `:<Boolean> 如果文件已正在监视，是否继续运行进程。默认为 `true`
    - `recursive`: <Boolean> 是否监视全部子目录。默认是 `false`
- `listener`:<Function> | <undefined> 默认为 undefined。
    - `eventType`:<String> 修改事件
    - `filename`:<String>  | <Buffer> 修改的文件名称


#### fs.access(path[,mode],callback) 判断文件的用户权限

- `path`: <string> | <Buffer> | <URL>
- `mode`:  <Inter> 默认为 fs.constants.F_OK ,可以是多个值，用`|`分开
- `callback` <Function>
    - `err`:<Error>
 
[更多`mode`说明](http://nodejs.cn/api/fs.html#fs_fs_constants_1)
```
// 检查文件是否存在。
fs.access(file, fs.constants.F_OK, (err) => {
  console.log(`${file} ${err ? '不存在' : '存在'}`);
});

// 检查文件是否可读。
fs.access(file, fs.constants.R_OK, (err) => {
  console.log(`${file} ${err ? '不可读' : '可读'}`);
});

// 检查文件是否可写。
fs.access(file, fs.constants.W_OK, (err) => {
  console.log(`${file} ${err ? '不可写' : '可写'}`);
});

// 检查文件是否存在且可写。
fs.access(file, fs.constants.F_OK | fs.constants.W_OK, (err) => {
  if (err) {
    console.error(
      `${file} ${err.code === 'ENOENT' ? '不存在' : '只可读'}`);
  } else {
    console.log(`${file} 存在且可写`);
  }
});
```
由于在使用`fs.access()`的前后可能被其他程序进行修改状态，所以建议在文件打开或者读取、写入状态下调用来判断
```
fs.open('myfile', 'wx', (err, fd) => {
  if (err) {
    if (err.code === 'EEXIST') {
      console.error('文件已存在');
      return;
    }

    throw err;
  }
 
});
```

### 文件流的操作

#### fs.createReadStream() 

- `path` <string> | <Buffer> | <URL>
- `options` <string> | <Object>
    - `flags` <string> 详见支持的 flag。默认为 'r'。
    - `encoding` <string> 默认为 null。
    - `fd` <integer> 默认为 null。文件描述符。
    - `mode` <integer> 默认为 0o666。
    - `autoClose` <boolean> 默认为 true。
    - `start` <integer>
    - `end` <integer> 默认为 Infinity。
    - `highWaterMark` <integer> 默认为 64 * 1024。
可读流的 highWaterMark 一般默认为 16 kb，但本方法返回的可读流默认为 64 kb。
 - 返回: 可读流。
```
var stream = fs.createReadStream(path)
stream.on("data",(chunk)=>{
    console.log(chunk)
})
```
#### fs.createWriteStream()

- path <string> | <Buffer> | <URL>
- options <string> | <Object>
    - flags <string> 详见支持的 flag。默认为 'w'。
    - encoding <string> 默认为 'utf8'。
    - fd <integer> 默认为 null。文件描述符。
    - mode <integer> 默认为 0o666。
    - autoClose <boolean> 默认为 true。
    - start <integer>
- 返回: 可写流。

如果指定`start`修位置，则默认的 `flags` 是 `r+`

```
var stream = fs.createWriteStream(path)
stream.write("helloworld","utf8")
```