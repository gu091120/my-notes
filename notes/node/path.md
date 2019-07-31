# node path

### path.basename(path[, ext])
- path: <String>
- ext:<String> 后缀
- return ：<String>

返回目标文件或者目录名称
```
var str = path.basename('/dir1/dir2/test.txt') //返回：text.txt
var str = path.basename('/dir1/dir2/test/') //返回：text
var str = path.basename('/dir1/dir2/test.text',".txt") //返回：text
```
在处理windows路径的时候，在不同的操作系统中会与不同的结果
```
//POSIX
path.basename('C:\\temp\\myfile.html');//返回：C:\\temp\\myfile.html

//Windows
path.basename('C:\\temp\\myfile.html') //返回：myfile.html

```
所以在处理Windows绝对路径时，需要用 `path.win32.basename`

### path.isAbsolute(path) 
判单是否是绝对路径

### path.join([...path])
返回拼接路径
```
path.join("./a","b") //返回：a/b
```

### path.reslove([...path])
返回拼接一个绝对路径
```
path.reslove("./a","b") //返回：/Users/gujieyi/learn/test/testB/a/b
```