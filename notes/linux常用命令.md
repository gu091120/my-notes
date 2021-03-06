# linux 常用命令:Ubuntu

## 系统命令

-   关机：poweroff
-   重启：reboot
-   查看用户系统信息 `lsb_release -a`

## ssh 登录

-   远程登录：`ssh [-p 22(默认端口号)] root(用户名)@108.10.1.2(ip地址)`
-   免密码登录

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

-   -r:遍历所有

解压文件
`unzip -o -d /home/file filename.zip`

-   -o:不提示覆盖
-   -d：指定解压目录

### tar

```
[root@www ~]# tar [-j|-z] [cv] [-f 创建的档名] filename... <==打包与压缩
[root@www ~]# tar [-j|-z] [tv] [-f 创建的档名]             <==察看档名
[root@www ~]# tar [-j|-z] [xv] [-f 创建的档名] [-C 目录]   <==解压缩
```

选项与参数：

- -c ：创建打包文件，可搭配 -v 来察看过程中被打包的档名(filename)
- -t ：察看打包文件的内容含有哪些档名，重点在察看『档名』就是了；
- -x ：解打包或解压缩的功能，可以搭配 -C (大写) 在特定目录解开
>  特别留意的是， -c, -t, -x 不可同时出现在一串命令列中。
- -j ：透过 bzip2 的支持进行压缩/解压缩：此时档名最好为 _.tar.bz2
- -z ：透过 gzip 的支持进行压缩/解压缩：此时档名最好为 _.tar.gz
- -v ：在压缩/解压缩的过程中，将正在处理的档名显示出来！
- -f filename：-f 后面要立刻接要被处理的档名！建议 -f 单独写一个选项罗！
- -C 目录 ：这个选项用在解压缩，若要在特定目录解压缩，可以使用这个选项。
 
其他后续练习会使用到的选项介绍：
- -p ：保留备份数据的原本权限与属性，常用於备份(-c)重要的配置档
- -P ：保留绝对路径，亦即允许备份数据中含有根目录存在之意；
- --exclude=FILE：在压缩的过程中，不要将 FILE 打包！

## 用户设置

### 账号管理

-   设置密码 `passwd`
-   添加新用户 `useradd -m(自动创建home文件) [username] ` 
-   切换用户 `su [username]`

### 权限管理

```
-rwxr--r--  1 root root 3107 May  8 10:30 .bashrc
1234567890  A   B   C     D       E        F

1 :"-"不是目录, "d"目录,"l"快捷方式 等
[234]:所属用户权限（r:可读(4), w:可写(2), x:可执行(1)）
[567]:所属同组用户权限
[890]:其他组用户权限

A:有多少档名连结到此节点
B:所属用户
C:所属用户组
D:文件大小（bt）
E:修改时间
F:文件签名（带点是隐藏文件）
```

> 权限 `x` 表示可执行，在文件目录表示是否可进入

#### 修改

-   chgrp:改变文件所属组
    ```
    chgrp [新的组名称] [文件名称]
    ```
-   chown:改变文件所属用户
    ```
    chown [用户名] [文件名]
    ```
-   chmod:改变文件权限
    ```
    chmod [权限值] [文件名]
    chmod 777 .bashrc //修改成所有用户都有全部权限
    ```

> 权限值： [-rwxr-xr--],表示：
>
> -   所属用户：rwx = 4+2+1 =7
> -   所属用户组用户：r-x = 4+0+1 =5
> -   其他组用户：r-- = 4+0+0 =4

## 文件管理

### 文件类型

-   正规文件（regular file）:在由 `ls` 展示出来的 第一个字符为 `-` 的文件
    -   纯文本（ASCII）：人能看懂的一些文件
    -   二进制文件（binary）：计算机直接执行的文件
    -   数据格式文件（date）：程序运行中读取的一些特殊格式的文件
-   目录（directory）(`d`)
-   快捷键（link）(`l`)
-   设备与装置文件（device）
    -   区块设备档（block）(`b`)
    -   字符设备文件（charactor）(`c`)
-   数据接口文件（sockets）(`s`)
-   数据输送文件（FIFO,pipe）(`p`)

重要的系统目录

-   `/bin`: 一般全部用户可调用指令`cat`、`chmod`、`mv`、 `mkdir`等
-   `/boot`:系统开机的主要文件
-   `/dev`:访问设备的接口
-   `/etc`:系统配置文件,比如：`hosts`
-   `/lib`:系统依赖的函数库
-   `/root`:root 用户的家目录
-   `/home`:系统默认用户的家目录
-   `/tmp`:存放程序执行的临时文件
-   `/sbin`:root 用户可执行的指令：`fdisk`、`shutdown`、`mount`
-   `/var`:系统执行中经常会发生变化的文件：系统日志(`var/log`,`var/message`)、程序或启动服务（`var/run`）
-   `/usr`:应用程序存放的目录 应用程序`/usr/bin/`

文件命令

## 进程管理

-   查询正在运行的进程 `ps -ef`
-   杀死进程 `kill -9 [进程编号]` -9:强制

## 软件操作

-   查看已安装软件：`dpkg -l [| grep ssh(文件名)]`

## vim 常用命令

-   v 第一次按 选择开始，第二下选择结束
-   V 选择整行
-   d 剪切
-   y 复制
-   p 粘帖
-   dd 删除整行

-   H 快速到全文开始处，并且切换成输入模式
-   M 快速到全文中间处，并且切换成输入模式
-   L 快速到全文中间处，并且切换成输入模式

-   /secharname ：简单搜索
-   :set hlsearch :高亮显示搜索结果
-   nohlsearch 关闭高亮

-   u 恢复最后一个指令之前的结果。
-   U 恢复游标该行之所有改变。
