# webpack 构建过程

webpack 的基本架构，是基于一种类似事件的方式[`Tapable`](/notes/webpack/Tapable认识.md),它的构建主要过程可以分为三个：

-   准备阶段
-   解析编译
-   整理输出

每个阶段通过不同hooks，调用不同的插件来完成。

![9f117920f34dcfbfcaf95c597c4b7085.gif](/notes/webpack/static/webpack流程图.svg)

## 准备阶段

- 初始化参数
- 实例化 Compiler,之后就会触发依次触发特定的hooks
- 加载插件(afterPlugins)
- 实例化输入输出(environment):输入:inputFileSystem,输出:outputFileSystem,是对node模块的`fs`模块的拓展。
```javascript

```
