# linux常用命令:Ubuntu

## 系统命令
- 关机：poweroff
- 重启：reboot
- 查看用户系统信息 `lsb_release -a`


## ssh 登录
- 远程登录：`ssh [-p 22(默认端口号)] root(用户名)@108.10.1.2(ip地址)`
- 免密码登录
```
//本机生成密钥
ssh-keygen -t rsa

//拷贝到远程计算机
ssh-copy-id -i ./.ssh/id_rea.pub root@10.50.67.12
```

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


## 进程管理 
- 查询正在运行的进程 `ps -ef`
- 杀死进程 `kill -9 [进程编号]` -9:强制  


## 软件操作
- 查看已安装软件：`dpkg -l [| grep ssh(文件名)]`


## vim 常用命令
- v   第一次按 选择开始，第二下选择结束
- V   选择整行
- d   剪切
- y   复制
- p   粘帖
- dd  删除整行

- H   快速到全文开始处，并且切换成输入模式
- M   快速到全文中间处，并且切换成输入模式
- L   快速到全文中间处，并且切换成输入模式

- /secharname ：简单搜索
- :set hlsearch :高亮显示搜索结果
- nohlsearch 关闭高亮

- u   恢复最后一个指令之前的结果。
- U   恢复游标该行之所有改变。