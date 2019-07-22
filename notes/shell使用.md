# shell 使用

## 基本概念

-   `Shell` : 是指一种用 C 语言编写的应用程序，这个应用程序提供了一个界面，用户通过这个界面访问操作系统内核的服务。可以理解计算机内核提供的人机交互的接口。
-   `shell script`:指为 `Shell` 这个应用编写的脚本，一般所说的就`shell` 就是指 `shell script`
-   `bash`: 是 `shell script` 解析器。

`Shell`的解析器：

-   linux 默认解析器`bash`
-   windows 默认没有解析器，可以下载 `git` 就代有 一个 `bash`
-   Mac 默认是 `bash`，推荐 [`on-my-zsh`](https://ohmyz.sh/)

## 语法

### 定义解析器：

```
#!/bin/bash
```

### 变量

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

- `/`:匹配第一个替换
- `//`:匹配全部替换 



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
