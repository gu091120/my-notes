# node http

## `http.createServer([options][, requestListener])`
- options <Object>
    - IncomingMessage <http.IncomingMessage> 指定使用的 IncomingMessage 类。
    - ServerResponse <http.ServerResponse> 指定使用的 ServerResponse 类。
- requestListener <Function> 自动注册 `request`监听器
- 返回: <http.Server> 

```
var httpServer = http.createServer(function(req,res){
   // req :http.IncomingMessage
   // res: http.ServerResponse
})
httpServer.listen(3030,function(){
    console.log("server is running")
})
```

### `http.Server`

#### `connection`事件
当建立tcp连接到时候触发

#### `request` 事件
当接收到http请求时，每个连接可能有多个请求（在 HTTP keep-alive 的情况下）。

### `server.setTimeout([msecs][, callback])`
- msecs <Number> 默认为 120000（2 分钟）。
- callback <Function>
- 返回: <http.Server>

设置服务超时时间

## `http.IncomingMessage`
http.IncomingMessage 对象由 http.Server 或 http.ClientRequest 创建，并作为参数分别传入 'request' 和 'response' 事件。 可以用来访问响应状态、消息头、或数据。实现了可读流接口。

#### `message.headers`
请求头（http.Server）或响应头（http.ClientRequest）的对象。

#### `close`事件
当底层tcp端口连接时触发，但是不代表没有数据返回


## `http.ServerResponse`
服务响应对象

#### `response.writeHead(statusCode[, statusMessage][, headers])`
- statusCode <number>
- statusMessage <string>
- headers <Object>

发送一个响应头给请求。 状态码是一个三位数的 HTTP 状态码，如 404。 最后一个参数 headers 是响应头。 第二个参数 statusMessage 是可选的状态描述。


#### `response.setHeader(name, value)`
- 设置响应头字段
- response.setHeader() 设置的响应头会与 response.writeHead() 设置的响应头合并，且 response.writeHead() 的优先。


#### `response.statusCode`
设置状态码



#### `response.write(chunk[, encoding][, callback])`
- chunk <string> | <Buffer>
- encoding <string> 默认为 'utf8'。
- callback <Function>
- 返回: <boolean>

写入输出流，该方法会发送一块响应主体。 它可被多次调用，以便提供连续的响应主体片段。

#### `response.end([data][, encoding][, callback])`
- data <string> | <Buffer>
- encoding <string>
- callback <Function>
- 返回: <http.ServerResponse>

 该方法会通知服务器，所有响应头和响应主体都已被发送，即服务器将其视为已完成。 每次响应都必须调用 response.end() 方法。
 
 
 
 ## `http.request(url[, options][, callback])`
 - url <string> | <URL>
- options <Object>

    - protocol <string> 使用的协议。默认为 http:。
    - host <string> 服务器的域名或 IP 地址。默认为 localhost。
    - hostname <string> host 的别名。为了支持 url.parse()，hostname 优先于 host。
    - family <number> 解析 host 和 hostname 时使用的 IP 地址族。值可以是 4 或 6。如果没有指定，则同时使用 IP v4 和 v6。
    - port <number> 远程服务器的端口。默认为 80。
    - localAddress <string> 网络连接绑定的本地接口。
    - socketPath <string> Unix 域 Socket。host:port 或 socketPath 二选一。
    - method <string> 请求的方法。默认为 'GET'。
    - path <string> 请求的路径。可以包括查询字符串，如 '/index.html?page=12'。如果请求的路径中包含非法字符，则抛出异常。默认为 '/'。
    - headers <Object> 请求头。
    - auth <string> 基本身份验证，如使用 'user:password' 计算 Authorization 请求头。
    - agent <http.Agent> | <boolean> 控制 Agent 的行为。可选的值有：

    - undefined (默认): 使用 http.globalAgent。
    - Agent: 使用传入的 Agent。
    - false: 新建一个使用默认配置的 Agent。
    - createConnection <Function> 如果没有指定 agent，则可用该函数为请求创建 socket 或流。这可以避免只是为了重写默认的 createConnection 而创建自定义的 Agent。详见 agent.createConnection()。
    - timeout <number>: socket 超时的毫秒数。
    - setHost <boolean>: 是否自动添加 Host 请求头。默认为 true。
- callback <Function>
- 返回: <http.ClientRequest>
    
发送 HTTP 请求。如果 url 是一个字符串，则自动使用 url.parse() 解析。 如果 url 是一个 URL, 则自动转换成 options 选项。

如果同时指定了 url 和 options，则合并两个对象，其中 options 优先。
```
const request = require("http").request;
const postData = "hello world";
const options = {
    hostname: "127.0.01",
    port: 8000,
    path: "/upload",
    method: "POST",
    headers: {
        "Content-Type": "application/x-www-form-urlencoded",
        "Content-Length": Buffer.byteLength(postData)
    }
};

var client = request(options, res => {
    //console.log(res.headers);
    res.on("data", chunk => {
        console.log(chunk + "");
    });
});

client.write(postData);
client.end();

```
#### `http.ClientRequest`
http.ClientRequest 实例由 http.request() 内部创建并返回。 表示一个正在进行中的请求，且请求头已进入队列。 请求头仍可使用 setHeader(name, value)、getHeader(name) 或 removeHeader(name) 进行修改。 最终的请求头会与第一个数据块一起发送或当调用 request.end() 时发送。

#### 'response' 事件
- response <http.IncomingMessage>
当请求的响应被接收到时触发。 该事件只触发一次。

## `http.Agent`
Agent 负责为 HTTP 客户端管理连接的持续与复用。 它为一个给定的主机与端口维护着一个等待请求的队列，且为每个请求重复使用一个单一的 socket 连接直到队列为空，此时 socket 会被销毁或被放入一个连接池中，在连接池中等待被有着相同主机与端口的请求再次使用。 是否被销毁或被放入连接池取决于 keepAlive 选项。