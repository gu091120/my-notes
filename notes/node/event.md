# event
#### eventEmitter.on(evenName,callBack) / prependListener

`on` 监听器数组中往后添加监听器，监听器会在每次触发命名事件时被调用,`prependListener`为监听数组中之前添加数组

#### eventEmitter.once(evenName,callBack) /prependOnceListener

也是注册监听器时，但是监听器只会触发一次命名事件时被调用
```
const myEmitter = new MyEmitter();
myEmitter.once("event",() =>{
    console.log(1)
})

myEmitter.on("event",() =>{
    console.log(2)
})

myEmitter.emit("event") // 打印: 1,2
myEmitter.emit("event") // 打印: 2
```

#### eventEmitter.removeListener(evenName,callBack)

去除监听器
```
const myEmitter = new MyEmitter();
const callback = () =>{
    console.log(1)
}
myEmitter.on("event",callback)

myEmitter.emit("event") // 打印: 1
myEmitter.removeListener("event",callback)
myEmitter.emit("event") // 不打印
```

#### eventEmitter.emit(evenName,arg,arg) 

触发已经监听的事件
```
const myEmitter = new MyEmitter();
myEmitter.on("event",(a,b) =>{
    console.log(a,b)
})

myEmitter.emit("event",1,2) //  打印:1,2
```


#### 已经存在事件

##### `error` 事件

当 EventEmitter 实例出错时，应该触发 'error' 事件。
如果没有为 'error' 事件注册监听器，则当 'error' 事件触发时，会抛出错误、打印堆栈跟踪、并退出 Node.js 进程。

```
const myEmitter = new MyEmitter();
myEmitter.on('error', (err) => {
  console.error('错误信息');
});
myEmitter.emit('error', new Error('错误信息'));
// 打印: 错误信息

```

##### 'newListener' 事件，'removeListener' 事件

当新增监听器时，会触发 'newListener' 事件；当移除已存在的监听器时，则触发 'removeListener' 事件。

```
const myEmitter = new MyEmitter();

const callback = () =>{
    console.log(1)
}

myEmitter.on("newListener",（event, listener）=>{
    console.log('添加新监听器', event, listener === callback)
})

myEmitter.on("removeListener",(event, listener)=>{
    console.log('删除监听器', event, listener === callback)
})// 打印: 添加新监听器 removeListener false

myEmitter.on('event',callback)// 打印: 添加新监听器 event true
myEmitter.removeListener("event",callback)// 打印: 删除监听器 event true

```

#### eventEmitter.listeners("event")
返回名为 eventName 的事件的监听器数组的副本。

```
const myEmitter = new MyEmitter();

const callback = () =>{
    console.log(1)
}

myEmitter.on("event",callback)

console.log(myEmitter.eventEmitter("event")[0] === callback) //打印：true
```

#### eventEmitter.removeAllListeners([listener])

移除全部监听器或指定的 eventName 事件的监听器。

