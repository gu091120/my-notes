# git 常用命令

## 常用操作

-   创建新分支 :git checkout -b [newbranchname]
-   将分支推送到远程仓库:git push --set-upstream origin
    [branchname]

-   版本会退:git reset --heard [版本号]
-   删除本地分支:git branch -d [branchname]
-   删除远程分支:git push origin --delete [branchname]
-   查看提交记录:git log -p -2

## 提交信息规范

```
<type>(scope): <subject>

<body>

<footer>

```

### message 格式

#### header

-   type

    -   ✨feature 或 feat: 引入新功能
    -   🐛fix: 修复了 bug
    -   📝docs: 文档
    -   🎨style: 优化项目结构或者代码格式
    -   ♻️refactor: 代码重构. 代码重构不涉及新功能和 bug 修复. 不应该影响原有功能, 包括对外暴露的接口
    -   ✅test: 增加测试
    -   ⏫chore: 构建过程, 辅助工具升级. 如升级依赖, 升级构建工具
    -   ⚡️perf: 性能优化
    -   ⏪ revert: revert 之前的 commit
    -   git revert 命令用于撤销之前的一个提交, 并在为这个撤销操作生成一个提交
    -   🎉 build 或 release: 构建或发布版本
    -   🔒 safe: 修复安全问题

-   scope: 可选. 说明提交影响的范围. 例如样式, 后端接口, 逻辑层等等

-   Subject: 提交目的的简短描述, 动词开头, 不超过 80 个字符. 不要为了提交而提交

#### body

可选. 对本次提交的详细描述. 如果变动很简单, 可以省略

#### footer

可选. 只用于说明不兼容变动(break change)和关闭 Issue(如果使用使用 gitlab 或 github 管理 bug 的话)

### 代码提交格式化

-   添加 prettier 依赖

```
yarn add prettier --dev --exact
```

-   测试格式化是否工作

```
yarn prettier -- --write src/index.js
```

-   在 commit 时执行 prettier

```
yarn add pretty-quick husky --dev
```

修改 package.json 添加 pre-commit 钩子

```
修改 package.json 添加 pre-commit 钩子
```

### 插件使用

-   conventional-changelog - 从项目的提交信息中生成 CHANGELOG 和发布信息
-   commitlint - 检验提交信息
-   commitizen - 🔥 简单的提交规范和提交帮助工具，推荐
-   standard-changelog - angular 风格的提交命令行工具

## 版本控制

### 分支模型

-   `master`:
    稳定版本，当`dev`分支完发布后，`master` 分支合并 `dev`，并且打上相应的版本 tag，一般开发人员没有合并 master 代码权限

-   `dev`:
    在一次版本迭代中，需要提交到新功能和 bug 的修复会提交到这里,然后发布测试环境

-   `feature/功能名称`:
    对应每次开发的功能，一般由`dev`分支而来

-   `preview`:
    对一些临时性需要在测试环境预览的功能，或者 bug 修复，一般使用后就销毁

-   `release/版本号`:
    一般稳定项目可以没有这个分支，这个分支主要是用来对某个应用版本的 bug 修复


## 发布工作流规范
![发布工作流规范.png](/notes/工作流程/static/发布工作流.png)

### 常用插件工具
- conventional-changelog-cli
- conventional-github-releaser

## 持续集成
### 持续
![发布工作流规范.png](/notes/工作流程/static/持续.png)
### 集成
![发布工作流规范.png](/notes/工作流程/static/集成.png)

## 任务管理

看板是目前最为流行的任务管理工具，它可以帮助我们了解项目的进度、资源的分配情况、还原开发现场.

- 基于issue看板 - 可以基于Gitlab或Github的Issue来做任务管理，它们都支持看板。很Geek，推荐
- Tower - 专门做看板任务管理的。小团队基本够用。我们现在就使用这款产品
- teambition - 和Tower差不多，没有深入使用过
- Trello - 颜值高.

### 参考
[看板系统实施细则](https://github.com/gu091120/kanban_enforcement)

