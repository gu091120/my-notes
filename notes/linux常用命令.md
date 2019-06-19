# linux常用命令

## 压缩

### zip
当前文件压缩
`zip -r name.zip ./*` 
- -r:遍历所有

解压文件
`unzip -o -d /home/file filename.zip`
- -o:不提示覆盖
- -d：指定解压目录


## 用户设置
- 设置密码 `passwd`
- 添加新用户 `useradd [username]`
- 切换用户 `su [username]`
- 查看用户系统信息 `lsb_release -a`



## 进程管理 
- 查询正在运行的进程 `ps -ef`
- 杀死进程 `kill -9 [进程编号]` -9:强制 