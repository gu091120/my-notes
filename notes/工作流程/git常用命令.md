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

### message type

-   feat：新功能（feature）
-   fix：修补 bug
-   docs：文档（documentation）
-   style： 格式（不影响代码运行的变动）
-   refactor：重构（即不是新增功能，也不是修改 bug 的代码变动）
-   test：增加测试
-   chore：构建过程或辅助工具的变动

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
