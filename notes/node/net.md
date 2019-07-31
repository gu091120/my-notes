# net 
node 创建tcp连接模块,主要是 `net.Server` 和 `net.Socket`

## 什么是`socket`
网络上的两个程序通过一个双向的通信连接实现数据的交换，这个连接的一端称为一个socket。

[更多内容](https://www.cnblogs.com/dolphinX/p/3460545.html)


## net.Server([options][,connectionListener])
- options <Object>
    - allowHalfOpen <Boolean> 表示是否允许一个半开的TCP连接, 默认值: false
    - pauseOnConnect <Boolean> 一旦来了连接，是否暂停套接字
- connectionListene  <Function> 为'connection'事件自动设置一个监听器。
- 返回：<net.Server>

创建一个tcp的服务端
```
var net = require("net");
var server = new net.Server();
server.on("connection", socket => {
    socket.on("data", res => {
        console.log("client_data:" + res);
    });
    socket.write("this is server");
    socket.on("close", () => {
        console.log("client is close");
    });
});
server.listen(3000, () => {
    console.log("server is running");
});

```
在`connection`的时候，回调函数参数是一个`net.Socket`类，是一个双工到的buffer

### net.createServer([options][, connectionListener])
一般我们使用的是`net.createServer`工厂函数来创建
```
var net = require("net");
var server = net.createServer();
server.on("connect",socket =>{
    socket.on("data",(res)=>{
        console.log("client_data:"+res)
    })
})
server.listen(3000, () => {
    console.log("server is run");
});

```

### server.close([callback])
关闭server，需要等到所有的`connection`都断开以后才会触发`close`事件

### server.getConections(callback(err,count))
异步获取服务器并发链接数


## new net.Socket([options])
创建一个`TCP`的Socket
- options <Object>
    - fd: <number> 如果指定了该参数，则使用一个给定的文件描述符包装一个已存在的 socket，否则将创建一个新的 socket。
    - allowHalfOpen <boolean> 指示是否允许半打开的 TCP 连接。
    - readable <boolean> 当传递了 fd 时允许读取 socket，否则忽略。默认 false。
    - writable <boolean> 当传递了 fd 时允许写入 socket，否则忽略。默认 false。
- 返回：<net.Socket>

```
var net = require("net");
var clientSockert = new net.Socket();
clientSockert.setTimeout(3000, function() {
    console.log("client:客户端超时");
    clientSockert.end("end");
});

clientSockert.connect(
    3000,
    "127.0.0.1",
    () => {
        clientSockert.write("this is client");
    }
);
```

### net.createConnection(port[, host][, connectListener])
- port <Number> 端口号
- host <String> IP地址或者域名
- connectListener <Function> 为'connect'事件自动设置一个监听器。
- 返回：<net.Socket>

一般我们使用这个工厂函数来创建`net.Socket`实例


### socket.setTimeout(timeout[, callback])
当一个闲置的超时被触发，socket 将会收到一个 'timeout' 事件，但连接不会被断开。用户必须手动调用 socket.end() 或 socket.destroy() 来断开连接。

### socket.end([data][, encoding][, callback])
- data <string> | <Buffer> | <Uint8Array>
- encoding <string> 仅当 data 是字符串时有效。默认为 'utf8'。
- callback <Function> 当 socket 完成时的回调函数。
- 返回: <net.Socket> socket 本身。

关闭写入流，但是服务端任然发送数据，读取流还是可以用的

### socket.destroy([exception])
确保在该 socket 上不再有 I/O 活动。仅在出现错误的时候才需要



