## 什么是`stream`

对数据输入输出的一个抽象

## 为什么要用 `stream`
在我们的需要是将一部电影返回给用户：
```
var fs = require('fs')
var http = require('http')
http.createServer((req,res)=>{
    fs.readFile(moviePath, (err, data) => {
        res.end(data);
    });
}).listen(8080)
```

这里就有几个问题：

- 读取文件需要很长时间，导致用户会等待很久，
- 读取的文件会很大，如果多个用户同时操作会占用极大的内存

用`stream`改写
```
var fs = require('fs')
var http = require('http')
http.createServer((req,res)=>{
    fs.createReadStream(moviePath).pipe(res)
}).listen(8080)
```
这样每次都是只取一部分返回客户端，就不会有让客户端等待太久，内存占用也是有限的。

## `stream`是如何解决问题

### `stream`分类

- 可读流：readable （例如：fs.createReadStream() ）
- 可写流：writable （例如：fs.createWriteStream() ）
- 可度可写流：duplex、transform

ps: node 中`stream` 是 `EventEmitter`接口的实现类

#### readable 
对于应用程序来说，可读取流可以看作：产生数据给程序使用的数据生产者。

在读取大数据的时候，并不是一次将数据读取出来，而是读取一部分，将这一部分放在内存中，并且当内存达到一定量（highWaterMark）的时候就会停止读取，直到数据被应用消费后清理出内存，才会再将读取数据放入内存。




##### 可读流有两种模式：
- 自动模式: 当数据内存没有达到 `highWaterMark` 自动生产数据
- 手动模式: 每次生产数据需要用过手动产生

当我们在 `data` 下注册监听器的时候，就默认开启了自动模式。而在`readable`下注册监听器的时候，则默认开启的是手动模式。

在自动模式下，我们可以通过`pause()`方法来暂停自动模式，暂停后可以通过手动模式生产数据。通过`resume()`方法,可以恢复自动模式。

##### 监听事件
-  `error` :当读取数据发生错误触发
-  `end` :数据读取完毕后触发


#### writable
对于应用来书，可写流可以看作：对产生的数据进行使用的消费者；

结合可读流，我们可以实现将读取的内容直接打印出来
```
var fs = require('fs')
var http = require('http')
var readStrem = fs.createReadStream(moviePath)
http.createServer((req,res)=>{
    readStrem.on("data",(trunk)=>{
        res.write(trunk)
    })
}).listen(8080)
```
但时候这里存在一个问题，当我们写入速度小于读取数据时候就会产生问题。
所以我们需要某个时刻告诉生产者暂时生产，和恢复生产。可写流，则提供了一个待写入数据的列队池，生产数据过快时就会，将这一部分数据存入。当`write()`超过  列队池的`highWaterMark`就会返回`false`来告诉生产者停止生成，当列队池的数据被消费掉以后就会触发`drain`事件来告诉生产者继续生成。当我们写完后，就需要通过`end()`来结束写入，使用和`write()`相同


这个时候我们就需要改写成：
```
var fs = require('fs')
var http = require('http')
var readStrem = fs.createReadStream(moviePath)
http.createServer((req,res)=>{
    var writeStream = res
    readStrem.on("data",(trunk)=>{
        if(res.write(trunk) === false){
            readStrem.pause()
        }
    })
    writeStream.on("drain",()=>{
         readStrem.resume()
    })
}).listen(8080)

```

这个也就是readable的`pipe()`实现过程

##### write(trunk[,encoding,callback])
- trunk ：写入数据（字符串或者buffer）
- encoding：编码（如果数据是字符串，可以设置编码，buffer 或者 object 模式会忽略）
- callback：数据写入后的回调函数，可以通知流传入下一个数据；当出现错误的时候也可以设置一个 error 参数

##### 监听的事件
-  `error` 当写入出现错误的时候触发
-  `finish` 调用 `end()`事件后,且队列池内的数据被读取完毕的时候触发
-  `pipe` 当可读流通过`pipe()`方法将数据流入可写流的时候触发
```
var fs = require('fs')
var readStrem = fs.createReadStream(moviePath)
var writerStream = process.stdout
writerStream.on('pipe',()=>{
    console.log("有数据流入可写流")
})
readStrem.pipe(writerStream) //打印：有数据流入可写流
```
-  `drain` 当队列池中数据被读取完的时候触发


#### `duplex、transform`
`duplex`:可以看作继承了`readable`和 `writable` 的实现类，重要的是输入和输出都是相互独立。
`transform`:时对输入和输出中间进行关联对数据进行加工。


### 参考：
- [https://www.cnblogs.com/dolphinX/p/6285240.html](https://www.cnblogs.com/dolphinX/p/6285240.html)
- [https://www.jianshu.com/p/81b032672223](https://www.jianshu.com/p/81b032672223)
    