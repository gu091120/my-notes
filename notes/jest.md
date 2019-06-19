#jest 使用

## 常用断言
-   相等断言
```
toBe(value)//字符串，数字
toEqual(value) //比较对象，非null，和undefind
toNull(value)
toBeUndefind(value)
```
-   包含断言
```
toHaveProperty(keyPath, value)： 是否有对应的属性
toContain(item)： 是否包含对应的值，括号里写上数组、字符串
toMatch(regexpOrString)： 括号里写上正则
```
-   逻辑断言
```
toBeTruthy()
toBeFalsy()
在JavaScript中，有六个falsy值：false，0，''，null， undefined，和NaN。其他一切都是Truthy。
toBeGreaterThan(number)： 大于
toBeLessThan(number)： 小于
toHaveBeenCalledTimes(number): 被调用次数
```
## 配置
可以在`webpack` 中配置，和 `jest.config.js` 中配置，如
```
module.exports = {
    testEnvironment:"node",
    moduleFileExtensions: ['js','json','jsx'],
    testMatch: ['**/__tests__/**/*.js?(x)','**/?(*.)(spec|test).js?(x)'],
    moduleNameMapper: {
    "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$":
        "<rootDir>/__mocks__/fileMock.js",
    "\\.(css|less)$": "<rootDir>/__mocks__/styleMock.js"
    }
}
```
#### 配置说明
-   testEnvironment ：设置测试环境 默认是`js的om`浏览器环境
-   testMatch： 匹配文件
-   moduleFileExtensions：拓展名
-   moduleNameMapper: 图片，css 等一些静态资源的代理。如何是适应 es6 的语法倒入 css 或者 less，需要 `npm i identity-obj-proxy --save-dev`
-   setupFiles:`jest`初始化设置（`>=react 16`,需要设置，不然会报错）
-   testURL：`jsdom` 环境下设置 url（`>=react 16`,需要设置，不然会报错）
```
setupFiles: ["./jest.setup.js"],
testURL: "http://localhost/",
moduleNameMapper: {
            "\\.(jpg|jpeg|png|gif|eot|otf|webp|svg|ttf|woff|woff2|mp4|webm|wav|mp3|m4a|aac|oga)$": "<rootDir>/__mocks__/fileMock.js",
            "\\.(css|less)$": "identity-obj-proxy"
        }
```
## 代码测试
### 异步代码测试几种实现方式
-   done
```
test('async',done =>{
    async((res)=>{
        expect(res).toBe(11)
        done()
    })
})
```
-   返回一个 promise 对象
```
test('async', () =>{
    return promisefun().then((res) => expect(res).toBe(11))
})
```
-   .resolves / .rejects
```
test('async', () =>{
    expect(promisefun()).resolves.toBe(11)
})
```
-   await
```
test('async', async () =>{
    const data = await promisefun()
    expect(data)toBe(11)
})
```
## 钩子
-   beforeEach: 在作用域范围内，每一次 `test` 之前都会执行一次
-   afterEach： 在作用域范围内，每一次 `test` 之后都会执行一次
-   beforeAll：在作用域范围内，所有 `test` 之前会执行一次
-   afterAll：在作用域范围内，所有 `test` 之后会执行一次
## `>= react 16` 注意点
-   需要`npm i enzyme-adapter-react-16 --save-dev`
-   需要 `testURL`和`setupFiles` 设置
```
//jest.setup.js
import { configure } from "enzyme";
import Adapter from "enzyme-adapter-react-16";
configure({
    adapter: new Adapter()
});
```
[参考](https://github.com/gu091120/myReactComponent/tree/master/g-redux)