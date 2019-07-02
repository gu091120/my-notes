# docker 使用
## 安装
- 自动脚本安装
```
$ curl -fsSL get.docker.com -o get-docker.sh
$ sudo sh get-docker.sh --mirror Aliyun
```

## 镜像 image
Docker 把应用程序及其依赖，打包在 image 文件里面。只有通过这个文件，才能生成 Docker 容器。image 文件可以看作是容器的模板。Docker 根据 image 文件生成容器的实例。同一个 image 文件，可以生成多个同时运行的容器实例。

image 是二进制文件。实际开发中，一个 image 文件往往通过继承另一个 image 文件，加上一些个性化设置而生成。举例来说，你可以在 Ubuntu 的 image 基础上，往里面加入 Apache 服务器，形成你的 image。
### 相关操作
- 查找镜像:`docker search [包含字段]`
- 获取镜像:`docker pull [ 仓库 ]:[ tag ]`
- 列出本地所有 image:`docker image ls`
- 删除某个 image :`docker rmi  [imagename]`
- 打包本地镜像, 使用压缩包来完成迁移:`docker save [ 镜像名 ] > [ 文件路径 ]`
- 导入镜像压缩包:`docker load < [ 文件路径 ]`
- 修改镜像tag:`docker tag [ 镜像名 or 镜像 id ] [ 新镜像名 ]:[ 新 tag ]`
- 登录/退出第三方仓库:`docker [ login/logout ] [ 仓库地址 ]`
- 推送镜像到仓库:`docker push [ 镜像名 ]:[ tag ]`

[官方image仓库](https://hub.docker.com/search?q=&type=image)


## 容器 container 
image 文件生成的容器实例，本身也是一个文件，称为容器文件。也就是说，一旦容器生成，就会同时存在两个文件： image 文件和容器文件。而且关闭容器并不会删除容器文件，只是容器停止运行而已。

### 容器生命周期管理
-  `docker run [OPTIONS] imagename`

> OPTIONS:
> - -d: 后台运行容器，并返回容器ID；
> - -i: 以交互模式运行容器，通常与 -t 同时使用；
> - -t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用
> - -p: 指定端口映射，格式为：主机(宿主)端口:容器端口
> - --name="nginx-lb": 为容器指定一个名称；
> - -e username="ritchie": 设置环境变量；
> - --env-file=[]: 从指定文件读入环境变量；
> - -m :设置容器使用内存最大值
> - --link=[]: 添加链接到另一个容器；
> - --expose=[]: 开放一个端口或一组端口；

>`举例`

使用镜像 nginx:latest，以后台模式启动一个容器,将容器的 80 端口映射到主机的 80 端口,主机的目录 /data 映射到容器的 /data。
```
docker run -p 80:80 -v /data:/data -d nginx:latest
```



- `docker start/stop/restart containername` :开始（已经停止的容器）/停止/重启一个或者多个docker
- `docker rm containername`:删除容器
- `docker exec [OPTIONS] containername`:

>OPTIONS:
> - -d :分离模式: 在后台运行
> - -i :即使没有附加也保持STDIN 打开
> - -t :分配一个伪终端

>`举例`

在容器 mynginx 中开启一个交互模式的终端:
```
docker exec -i -t  mynginx /bin/bash
```
