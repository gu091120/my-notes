# git常用命令

## 常用操作
- 创建新分支 :git checkout -b [newbranchname] 
- 将分支推送到远程仓库:git push --set-upstream origin [branchname]
- 删除本地分支:git branch -d [branchname]
- 删除远程分支:git push origin --delete [branchname]
- 查看提交记录:git log -p -2

## message type
- feat：新功能（feature）
- fix：修补bug
- docs：文档（documentation）
- style： 格式（不影响代码运行的变动）
- refactor：重构（即不是新增功能，也不是修改bug的代码变动）
- test：增加测试
- chore：构建过程或辅助工具的变动