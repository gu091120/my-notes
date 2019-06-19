# 浏览器和Node事件循环的区别
## node (10以前）
#### 主要阶段：
- timer ：定时器
- i/o ：完成i/o后的时间事件回调
- check：setImmediate
其他任务
- process.nextTick() (优先级大)
- promise()

``` JavaScript
//执行顺序:
while (true) {
    loop.forEach((阶段) => {
        nextTick全部任务();
        promise全部任务();
        阶段全部任务();
    });
    loop = loop.next;
}
```

### windows环境
- microTask（微任务）
    - Promise
    - Object.observe
    - MutationObserver。 
- macroTask（宏任务）
    - script 中代码
    - setTimeout
    - setInterval
    - I/O
    - UI render
    
``` JavaScript
while (true) {
    微任务队列全部任务();
    宏任务队列.shift();
}
```
