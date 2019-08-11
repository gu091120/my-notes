# shell 使用

## 基本概念

-   `Shell` : 是指一种用 C 语言编写的应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。可以理解计算机内核提供的人机交互的接口。
-   `shell script`:指为 `Shell` 这个应用编写的脚本，一般所说的就`shell` 就是指 `shell script`
-   `bash`: 是 `shell script` 解析器。

`Shell`的解析器：

-   linux 默认解析器`bash`
-   windows 默认没有解析器，可以下载 `git` 就代有 一个 `bash`
-   Mac 默认是 `bash`，推荐 [`on-my-zsh`](https://ohmyz.sh/)

### login 与 non-login shell

## 语法

### 定义解析器：

```
#!/bin/bash
```

### 变量

### `$`变量
 - `$$`:Shell本身的PID（ProcessID）
 - `$!`:Shell最后运行的后台Process的PID
 - `$?`:最后运行的命令的结束代码（返回值）
 - `$0`:执行路径相对被执行的文件路径文件地址包括文件名称
 - `$#`:执行的参数个数
 - `$*`:执行的输出全部参数以一个字符串形式输出
 - `$@`:执行的输出全部参数以有空格的字符串的形式输出
 - `$1`:执行的第一参数
 - `$2`:执行的第二参数


#### 变量类型

-   环境变量（全局变量） :`env`来查看当前环境变量。

    -   `HOME`:用户主目录
    -   `PATH`:Shell 查找命令的目录列表，由冒号分隔

    ```
    #添加环境变量
    path=$PATH:/other/bin
    export $path
    ```

-   自定义变量（局部变量）:`set`查看自定义变量。

    -   `?`:关于上个运行命令的回传值,一般成功会是 0。
    -   `$`:当前进程 id

    自定义变量可以在 `HOME`路径下的 `.bashrc` 文件配置（non-login shell 会读）

> 环境变量和自定变量区别，自定义变量不能被`子 bash`继承，但是可以通过 `export`转为零时环境变量

#### 定义变量

```
#!bin/bash

name="xiaoming"
echo ${name}

# name只读
readonly name

#删除 name
unset name

```

#### `read` 键盘输入变量

```
#!/bin/bash

read name

echo $name

```

#### 匹配删除与替换

```
#!/bin/bash
path=/usr/bin:/usr/sdf/bin:/dfaf/bin:/ss/
echo ${path#/*bin:}
# /usr/sdf/bin:/dfaf/bin:/ss/

echo ${path##/*bin:}
# /ss/

echo ${path%/bin:*}
# /usr/bin:/usr/sdf/bin/:/dfaf

echo ${path%%/bin:*}
# /usr

echo ${path/bin/BIN}
/usr/BIN:/usr/sdf/bin:/dfaf/bin:/ss/

echo ${path//bin/BIN}
/usr/BIN:/usr/sdf/BIN:/dfaf/BIN:/ss/
```

删除

-   `*`:通配符号
-   `#`:向左匹配，最短的
-   `##`:向左匹配，最长的
-   `%`:向右匹配，最短的
-   `%%`:向左匹配，最长的

替换

-   `/`:匹配第一个替换
-   `//`:匹配全部替换

其他

-   \# 注释符号：这个最常被使用在 script 当中，视为说明！在后的数据均不运行
-   \ 跳脱符号：将『特殊字符或通配符』还原成一般字符
-   | 管线 (pipe)：分隔两个管线命令的界定(后两节介绍)；
-   ; 连续命令下达分隔符：连续性命令的界定 (注意！与管线命令并不相同)
-   ~ 用户的家目录
-   \$ 取用变量前导符：亦即是变量之前需要加的变量取代值
-   & 工作控制 (job control)：将命令变成背景下工作
-   ! 逻辑运算意义上的『非』 not 的意思！◊
-   / 目录符号：路径分隔的符号
-   \> , >> 数据流重导向：输出导向，分别是『取代』与『累加』
-   <, << 数据流重导向：输入导向
-   ' ' 单引号，不具有变量置换的功能
-   " " 具有变量置换的功能！
-   `` 两个『 ` 』中间为可以先运行的命令，亦可使用 \$( )
-   ( ) 在中间为子 shell 的起始与结束
-   { } 在中间为命令区块的组合！

#### 数据流处理

##### cut

```
[root@www ~]# cut -d'分隔字符' -f fields <==用于有特定分隔字符
[root@www ~]# cut -c 字符区间            <==用于排列整齐的信息
```

选项与参数：

-   -d ：后面接分隔字符。与 -f 一起使用；
-   -f ：依据 -d 的分隔字符将一段信息分割成为数段，用 -f 取出第几段的意思；
-   -c ：以字符 (characters) 的单位取出固定字符区间；

##### grep

```
[root@www ~]# grep [-acinv] [--color=auto] '搜寻字符串' filename
```

选项与参数：
-a ：将 binary 文件以 text 文件的方式搜寻数据
-c ：计算找到 '搜寻字符串' 的次数
-i ：忽略大小写的不同，所以大小写视为相同
-n ：顺便输出行号
-v ：反向选择，亦即显示出没有 '搜寻字符串' 内容的那一行！
--color=auto ：可以将找到的关键词部分加上颜色的显示喔！


##### awk

```
[root@www ~]# awk '条件类型1{动作1} 条件类型2{动作2} ...' filename
```

内置变量




### 数组

```
#!/bin/bash
arr=(ar1  ar2 ar3)
echo ${arr[0]} //ar1
echo ${arr[@]} //ar1 ar2 ar3

```

### 运算

```
!/bin/bash

sum=`expr 1 + 2`
echo sum //3

```

-   `${a} -gt ${b}` : a > b
-   `${a} -it ${b}` : b < a
-   `${a} -ge ${b}` : a >= b
-   `${a} -ie ${b}` : b <= a

文件测试运算符

```

#!/bin/bash
file="/var/www/runoob/test.sh"
if [ -r $file ]
then
echo "文件可读"
else
echo "文件不可读"
fi
if [ -w $file ]
then
echo "文件可写"
else
echo "文件不可写"
fi
if [ -x $file ]
then
echo "文件可执行"
else
echo "文件不可执行"
fi
if [ -f $file ]
then
echo "文件为普通文件"
else
echo "文件为特殊文件"
fi
if [ -d $file ]
then
echo "文件是个目录"
else
echo "文件不是个目录"
fi
if [ -s $file ]
then
echo "文件不为空"
else
echo "文件为空"
fi
if [ -e $file ]
then
echo "文件存在"
else
echo "文件不存在"
fi

```

### 流程控制

-   if-else

```

if [ ${a} > ${b}]
then
echo "a > b"
elif [ ${a} = ${b} ]
then
echo "b = a"
else
echo "a < b"
fi

```

-   for

```

arr=(1 2 3)
for item in ${arr}
do
    echo ${item}
done

```

-   while

```

\$int=1

while(${int}<=5)
do
 echo ${int}
let "int++"
done

```

### 函数

```

sum(){
echo `expr ${0} + ${1}`
}
sum 1 2 //3

```

### 流的控制

```

```

```

```
