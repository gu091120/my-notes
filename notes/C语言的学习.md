# C语言的学习

## 环境搭建（vscode）

- 安装vscode
- 安装 C/C++ 插件
- 安装编译、调试环境
    - [下载MinGW](http://mingw.org/)
    - 设置全局变量
- 在vscode `.vscode`文件中新建：
    - launch.json（F5调试配置）
    ```
    {
        "version": "0.2.0",
        "configurations": [
            {
                "name": "(gdb) Launch",
                "type": "cppdbg",
                "request": "launch",
                "program": "${workspaceFolder}/hello.exe", //执行入口文件
                "args": [],
                "stopAtEntry": false,
                "cwd": "${workspaceFolder}",
                "environment": [],
                "externalConsole": true,
                "MIMode": "gdb",
                "miDebuggerPath": "C:\\MinGW\\bin\\gdb.exe", //安装MinGW文件地址
                "preLaunchTask":"gcc", //自动编译脚步名称
                "setupCommands": [
                    {
                        "description": "Enable pretty-printing for gdb",
                        "text": "-enable-pretty-printing",
                        "ignoreFailures": true
                    }
                ]
            }
        ]
    }
   
    ```
    
    - tasks.json(自动编译)

    ```
    {  
        "version": "2.0.0",  
        "command": "gcc",  
        "args": ["-g","hello.c","-o","${fileBasenameNoExtension}.exe"],    // 编译命令参数  
        "problemMatcher": {  
            "owner": "c",  
            "fileLocation": ["relative", "${workspaceRoot}"],  
            "pattern": {  
                "regexp": "^(.*):(\\d+):(\\d+):\\s+(warning|error):\\s+(.*)$",  
                "file": 1,  
                "line": 2,  
                "column": 3,  
                "severity": 4,  
                "message": 5  
            }  
        }  
    }  
    ```

- 调试 
    -   代码

    ```
    #include <stdio.h>
    int main(){
        char a = 121；
        printf("hello world");
        printf("hello world");
        printf("hello world");
        return 0 ;
    }
    ```
    -   `ctrl`+F5(打断点控制台不会立马消失)

>tip：解决中文输出乱码，设置vsocode编码格式 `gb2312`

## 基本语法
###  程序结构
```
#include <stdio.h> //依赖引入
 
int main() //主要执行的方法
{
   /* 我的第一个 C 程序 */ //注释
   printf("Hello, World! \n");
   
   return 0;
}
```

### 数据类型
#### 基本类型

> 说明：1b（字节）= 2^8  |  1kb = 1024b  |  1M = 1024kb |  1G = 1024m

- 字符
    - char ：`1b` 表示一个字符

- 整数
    -   short: `2b` 值范围：-32,768 到 32,767
    -   int : `2b/4b` 值范围：-32,768 到 32,767,767 或者 483,648 到 2,147,483,647
    -   long：`4b` 值范围：-2,147,483,648 到 2,147,483,647
    -   unsigned short：`2b` 值范围：0 到 65,535
    -   unsigned int：`2b/4b` 值范围：0 到 65,535 或 0 到 4,294,967,295
    -   unsigned long：`4b` 值范围：0 到 4,294,967,295
  
- 浮点数
    -   fload : `4b` 值范围:	1.2E-38 到 3.4E+38(6位小数)
    -   dobule: `8b` 值范围：   1.2E-38 到 3.4E+38（15位小数）
    -   long double: `16b` 值范围：3.4E-4932 到 1.1E+4932（19位小数）
> tip: sizof(type) 来判断类型所占位数
```
#include <stdio.h>
int main(){
     printf("int 存储大小\0: %lu \n", sizeof(int));
     return 0;
}
```

>tip: 关于printf()输出技巧`%[对齐方式-（向左）] [占的最小位数] [类型（d:10进制整数，f:6位小数浮点数，c:单个字符，s：字符串）]`
```
#include <stdio.h>
int main(){
    int a=2;
    fload b = 3.01;
    char c = '@';
    char *d = "hello world";
    printf("%-2d%3f%-2c%-3s")
    return 0
}
```




#### void 类型
void 类型指定没有可用的值。它通常用于以下三种情况下：
- 	函数返回为空：C 中有各种函数都不返回值，或者您可以说它们返回空。不返回值的函数的返回类型为空。例如 void exit (int status);
-   函数参数为空：C 中有各种函数不接受任何参数。不带参数的函数可以接受一个 void。例如 int rand(void);
-   指针指向 void： 类型为 void * 的指针代表对象的地址，而不是类型。例如，内存分配函数 void *malloc( size_t size ); 返回指向 void 的指针，可以转换为任何数据类型。

#### 构造类型

- 枚举类:枚举默认的值是从`0`开始，也是初始化定义第一个默认值，后面的会依次叠加。
    - 适用；更好的管理常量

    - 定义方式：
        1. 定义枚举类型后声明枚举变量
        
        ```
        int main(){
            enum WEEk {Won=1,Tuse,Wed,Thurs,Fir,Sat,Sum};
            emum WEEK day = Thurs;
            printf("%d",day); //4
            return 0;
        }

        ```
        2. 定义枚举类型的同时声明枚举变量
        
        ```
         int main(){
            enum WEEk {Won=1,Tuse,Wed,Thurs,Fir,Sat,Sum} day;
            day = Thurs;
            printf("%d",day); //4
            return 0;
        }
        ```

        3. 定义枚举类型的同时利用typedef关键字将其声明为类型别名，然后利用该类型别名声明枚举类型变量

         ```
         int main(){
            typedef enum WEEk {Won=1,Tuse,Wed,Thurs,Fir,Sat,Sum} WEEk;
            WEEk day = Thurs;
            printf("%d",day); //4
            return 0;
        }
        ```
    


- 数组类
- 结构体类型
- 共用体类型


#### 指针类型


### 常量、变量

#### 常量

基本类型都可以常量
- 定义：
关键字`const`或者`define`
```
#include <stdio.h>

#define  LIGHT 10
#define  HIGHT 20

int main(){
    const int COUNT = 10;
    const char S= 's';
    return 0
}
```
- 区别 ：
    -   `define`：又叫宏定义的常量，编译的时候直接将值替换成常量

### 类型转换
- 自动转换
 
har => int => fload :char 转 int 字符转成Unicode编码，占有字节小的可以向字节大的转，反之则不可以
```
char s = '@';
int c = s; //c=64
fload f = c; //f = 64

```

- 强制转换
公式：  类型  接受目标 = （目标类型）转换目标：转换时，不会改变目标类型

```
dobule d = 1.1222
int i = (int) d
printf("%d",i) //1
```

### 变量存储类
#### 动态变量
- 全局动态变量:

    -   `生命周期`:程序运行开始到结束；
    -   `作用域`：整个项目；
    -   `初始值`：如果没有显示初始化，其值为：0；
    

- 局部动态变量：

    -   `生命周期`:从函数被调用到函数退出。如果没有显示初始化，其值为：随机值；
    -   `作用域`：当前函数内部；
    -   `初始值`：如果没有显示初始化，其值为：随机值；

> PS :关键字`register`：变量存储大位置不是在内存，而是CPU的寄存器（可以大大提高运算效率）。注意：只能在局部使用，而且个数是有限制的。



#### 静态变量 

- 全局静态变量：
    
    -   `生命周期`:程序运行开始到结束。如果没有显示初始化，其值为：0;
    -   `作用域`：所在源文件内部;
    -   `初始值`：如果没有显示初始化，其值为：0；

- 局部静态变量：

    -   `生命周期`:程序运行开始到结束，当函数再次被调用时，局部静态变量不会重新创建，而是延用上次的值；
    -   `作用域`：所在函数内部;
    -   `初始值`：如果没有显示初始化，其值为：0；


