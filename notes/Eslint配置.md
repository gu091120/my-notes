# Eslint配置

## `react`项目 配置
```
module.exports = {
    env: {
        browser: true,
        commonjs: true,
        es6: true
    },
    globals: { //全局变量
        __DEV__: true,
        U: true
    },
    extends: [
    		"eslint:recommended", //默认推荐配置
    		"plugin:react/recommended" //react 插件
    ], 
    parserOptions: {
        ecmaVersion: 6,
        sourceType: "module",
        ecmaFeatures: { jsx: true, modules: true }
    },
    parser: "babel-eslint", //编译器选择
    plugins: ["react"],
    rules: {
        //indent: ["error", "tab"],
        "linebreak-style": ["error", "unix"],
        quotes: ["error", "double"],
        //semi: ["error", "always"],
        "no-console": "off",
        "no-mixed-spaces-and-tabs": "off"
    }
}
```
## webpack
```
{
 	rules:[
 		{
 			test:\/.jsx?$\,
 			include:[path],
 			use:['babel-loader',"eslint-loader"] //确保eslint-loader 在 babel-loader 之前
 		}
 	]
}
```