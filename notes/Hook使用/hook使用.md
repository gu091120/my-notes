# hook 使用

## useCallback(fun,[dep]) ：缓存函数,避免每次刷车重新生成函数,并且缓存函数运行状态

```javascript
const fun = (a, b) => a + b;
const addFun = useCallback(fun, [a, b]); 
```
## useMemo

## useImperativeHandle

## useLayoutEffect

## useDebugValue
