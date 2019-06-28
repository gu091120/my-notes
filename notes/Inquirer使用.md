# Inquirer使用

## 说明

给用户提供了一个漂亮的界面和提出问题流的方式:

- 提供错误回调
- 询问操作者问题
- 获取并解析用户输入
- 检测用户回答是否合法
- 管理多层级的提示

## 安装
```
npm install inquirer
```
### demo


```
var inquirer = require('inquirer')
inquirer.prompt([
  {
    type: 'confirm',
    name: 'test',
    message: 'Are you handsome?',
    default: true
  }
]).then((answers) => {
  console.log('结果为:')
  console.log(answers)
})
```

## inquirer.prompt(questions) => Promise

启动一个问答提示框，返回的是一个Promise对象

### questions

- type:String , 表示提问类型
  - list : 问题对象中必须有type,name,message,choices等属性，同时，default选项必须为默认值在choices数组中的位置索引(Boolean) 
  - rawlist: 与List类型类似，不同在于，list打印出来为无序列表，而rawlist打印为有序列表
  - expand: 同样是生成列表，但是在choices属性中需要增加一个属性：key，这个属性用于快速选择问题的答案。类似于alias或者shorthand的东西。同时这个属性值必须为一个小写字母
   ```
  {
    choices:[{key:"x",name:"name",value:1}]
  }
  ```
  - checkbox: 其余诸项与list类似，主要区别在于，是以一个checkbox的形式进行选择。同时在choices数组中，带有checked: true属性的选项为默认值。
  ```
  {
    choices:[{checked:true,name:"name",value:1}]
  }
  ```
  - confirm: 提问，回答为Y/N。若有default属性，则属性值应为Boolean类型
  - input :获取用户输入字符串
  - password: 与input类型类似，只是用户输入在命令行中呈现为*****
  - editor:终端打开用户默认编辑器，如vim，notepad。并将用户输入的文本传回
- name:String answers对象的key
- message: String|Function,  打印出来的问题标题，如果为函数的话
- default: String|Number|Array|Function,  用户不输入回答时，问题的默认值。或者使用函数来return一个默认值。假如为函数时，函数第一个参数为当前问题的输入答案。
- choices: Array|Function,  给出一个选择的列表，假如是一个函数的话，第一个参数为当前问题的输入答案。为数组时，数组的每个元素可以为基本类型中的值。
- validate: Function,  接受用户输入，并且当值合法时，函数返回true。当函数返回false时，一个默认的错误信息会被提供给用户。
- filter: Function,  接受用户输入并且将值转化后返回填充入最后的answers对象内。
- when: Function|Boolean,  接受当前用户输入的answers对象，并且通过返回true或者false来决定是否当前的问题应该去问。也可以是简单类型的值。
- pageSize: Number,  改变渲染list,rawlist,expand或者checkbox时的行数的长度。

## inquirer.registerPrompt(name,prompt)
注册提示插件


