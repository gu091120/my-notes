# Tapable

提供各种类型的 `hooks`

## api 分类

### 钩子类型

-   同步类（sync）
    -   SyncHook(串行同步执行，不关心事件处理函数的返回值)
    -   SyncBailHook(串行同步执行，如果事件处理函数执行时有一个返回值不为空（即返回值为 undefined），则跳过剩下未执行的事件处理函数)
    -   SyncWaterfallHook(串行同步执行，上一个事件处理函数的返回值作为参数传递给下一个事件处理函数，依次类推)
    -   SuncLoopHook(为串行同步执行，事件处理函数返回 true 表示继续循环，即循环执行当前事件处理函数，返回 undefined 表示结束循环)
-   异步类（async）
    -   AsyncParalle\*(并行)
        -   AsyncParallelHook(异步并行执行)
        -   AsyncParallelBailHook(异步并行执行,如果事件处理函数执行时有一个返回值不为空（即返回值为 undefined），则跳过剩下未执行的事件处理函数)
    -   AsyncSeries\*(串行)
        -   AsyncSeriesHook(异步串行执行)
        -   AsyncSeriesBailHook(异步串行执行,如果事件处理函数执行时有一个返回值不为空（即返回值为 undefined），则跳过剩下未执行的事件处理函数)
        -   AsyncSeriesWaterfallHook(异步串行执行,上一个事件处理函数的返回值作为参数传递给下一个事件处理函数，依次类推)

#### demo

```javascript
const SyncHook = require("SyncHook");
const hook = new SyncHook(["arg1", "arg2", "arg3"]);
```

### 注册事件/触发

    - 同步类（sync）
        - tap/call
    - 异步类（async）
        - tapAsync/callAsync
        - tapPromise/promise

#### demo

```javascript
const SyncHook = require("SyncHook");
const hook = new SyncHook(["arg1", "arg2", "arg3"]);

//注册
hook.tap("evenName", (arg1, arg2, arg3) => {
    // do somethings
});

//触发
hook.call("arg1", "arg2", "arg3");
```

### 拦截器

    - intercept
        - call : 当你的钩子触发之前,(就是call()之前),就会触发这个函数,你可以访问钩子的参数.多个钩子执行一次
        - tap :每个钩子执行之前(多个钩子执行多个),就会触发这个函数
        - loop: 这个会为你的每一个循环钩子(LoopHook, 就是类型到Loop的)触发,具体什么时候没说
        - register:每添加一个Tap都会触发 你interceptor上的register,你下一个拦截器的register 函数得到的参数 取决于你上一个register返回的值,所以你最好返回一个 tap 钩子(如果注册多个的话)

#### demo

```javascript
const SyncHook = require("SyncHook");
const hook = new SyncHook(["arg1", "arg2", "arg3"]);

hook.intercept({
    call:(...args)=>{

    },
    tap:(tapInfo)=>{

    },
    loop:(...args)=>{

    }
    register:(tapInfo)=>{

    }
})

//注册
hook.tap("evenName", (arg1, arg2, arg3) => {
    // do somethings
});

//触发
hook.call("arg1", "arg2", "arg3");
```

### context

插件和拦截器都可以选择加入一个可选的 context 对象, 这个可以被用于传递随意的值到队列中的插件和拦截器.

在`intercept`开启

```javascript
hook.intercept({
    context: true,
    call: (context, tapInfo) => {
        //context,这个字段
        context.isShow = false;
    }
});

hook.tap({ name: "dmo1", context: true }, (context, ...args) => {
    if (context.isShow === true) {
        //do somethings
    }
});
```

### HookMap

一个 HookMap 是一个 Hooks 映射的帮助类
```javascript
const keyedHook = new HookMap(key => new SyncHook(["arg"]))
keyedHook.tap("keyName","name",(arg)=>{

})
keyedHook.get.intercept({})
keyedHook.get("keyName").call("arg")

```


