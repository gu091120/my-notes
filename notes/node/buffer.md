
 ## 什么是Buffer
一个存储unicode码位的类数组对象，提供对数据内存申请、创建和操作的方法。类似于`ArrayBuffer`的直接视图
```
var buf = Buffer.from("123");
console.log(buf); //<Buffer 31 32 33>
```

 ## 主要作用
#### 处理二进制

js语言自身只有字符串数据类型，没有二进制数据类型，而处理TCP和文件流的时候，必须处理二进制数据

#### 大内存操作
##### 内存分配
`buffer`对象内存实际分配不在 `v8`的堆内存中，而是由C++层实现内存的申请，采用的`slab`分配机制(大于8kb为大内存，否则就是小内存)，所以是不占node运行的内存（node默认运行最大内存：64位，大约1.4G，32位：大约。0.7G）

##### 小内存：每个小内存有3中状态（完全分配，部分分配，没有分配）。
- 部分内存在`Buffer.allocUnsafe()`方法创建内存时，会有可能被存入新的数据，所以在新创建的内存会存有旧 的信息，所以是不安全。但是少了申请、创建过程所以会比`Buffer.alloc`创建的速度快很多。
- 在内存的回收中，存有多个buffer对象在作用域都被释放是才能能被回收，所以`Buffer.allocUnsafe()`创建的`buffer`对象在内存回收是比较慢的

##### 大内存：会直接分配一个 `SlowBuffer`对象，buffer模块可以直接访问和操作它，但是不推荐。

## 创建一个buffer
##### `Buffer.alloc(size,[fill,encoding])`

`size`:定义长度（定义后不可变）

`fill`:填充

`encoding`:编码类型
```
var buf = Buffer.alloc(9,"你好","utf-8")
console.log(buf.toString()) //"你好你"
```
##### `Buffer.allocUnsafe()`

和`Buffer.alloc`用法相同，最大的区别在于前者创建速度比后者快，但是后者创建时数据可能代用其他内存的信息，所以存在安全问题

##### `Buffer.from()`
- `Buffer.from(array)`
`array`:[unicode码位,unicode码位]

unicode码位：number类型
```
var arr = "buffer".split("").map(i=>i.charCodeAt())
var buf = Buffer.from(arr)
console.log(buf.toString()) //"buffer"

```

 #####  `Buffer.from(arrayBuffer[, byteOffset[, ]])`
 会得到`arrayBuffer`的内存共享，
 
`byteOffset`:开始位置

`length`:共享的长度
```
var buffer = new ArrayBuffer(8);
var view = new Int32Array(buffer);
view[0] = 1000;
var buf = Buffer.from(view.buffer);
console.log(buf); //<Buffer e8 03 00 00 00 00 00 00>
view[0] = 2000;
console.log(buf); //<Buffer d0 07 00 00 00 00 00 00>

console.log(view.buffer === buf.buffer ) //true
```

##### `Buffer.from(object[, offsetOrEncoding[, length]])`

`object`:支持 `Symbol.toPrimitive` 或 `valueOf()`的对象(number是不行的)

`offsetOrEncoding`:类型或者偏移量

`length`:长度

##### 注意：由于`new Buffer`创建内存不确定可能带有其他数据，所以官方已经不推荐使用

## Buffer的转换

##### `buf.toString([encoding,start,end])`
```
//字符串 =>Buffer
var buf = Buffer.from("123");
console.log(buf); //<Buffer 31 32 33>

//Buffer =>字符串
console.log(buf.toString()) //"123"

```
##### 支持类型 
- ASCII
- UTF-8
- UTF-16/UCS-2
- Base64
- Binary
- Hex

通过`Buffer.isEncoding(encoding)`来判断

对于不支持的类型可以通过iconv（c++的libiconv）和iconv-list(纯js实现，少了转码，所以性能比较前者要高)
```
var icon = require("iconv-lite");
var buf = icon.encode("123", "win1251");

console.log(Buffer.isBuffer(buf)); //true
var str = icon.decode(buf, "win1251");
console.log(str); //123

```
##### `buffer.transcode(source, fromEnc, toEnc)`

将一种编码转换到另一种编码
```
var buffer = require("buffer");
var buf = Buffer.from("€");
var rt = buffer.transcode(buf, "utf8", "ascii");
console.log(rt.toString()); //"?"
```





## Buffer的写入
##### buf.write(string[, offset[, length]][, encoding])
```
var buf = Buffer.alloc(10);
buf.write("123")
console.log(buf.toString()) //"123"
```

## 其他常用静态方法

##### `Buffer.concat(list[, totalLength])`
- list: `<Buffer[]>` | `<Uint8Array[]>` 要合并的 ` Buffer` 数组或 Uint8Array 数组。
- totalLength: `<integer>` 合并后 Buffer 的总长度。
#####  `Buffer.compare(buf1, buf2)`比较两个buffer对象


## Buffer 实例方法属性
##### `buf.equals(otherBuffer)`

比较两个buffer对象是否相等
 






