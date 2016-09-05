# 部署

以下部署方法均以默认 `fs` 插件为例。

## 方式 1: 在你的 VPS 上编译

1. `go get github.com/7sDream/rikka`
2. `cd $GOPATH/src/github.com/7sDream/rikka`
3. `go build github.com/7sDream/rikka`
4. `./rikka --port 80 --pwd yourpassword`

最后一步具体的命令可查看 `./rikka -h` 之后根据自己需要设置。因为要使用 80 端口，所以可能需要 `sudo`。

之后你就可以用浏览器打开看看效果了。

## 方式 2: 使用 Docker

1. `docker pull 7sdream/rikka`
2. `docker run -d -P 7sdream/rikka:latest -pwd yourpassword`

同样可以根据需要设定参数。

打开浏览器访问你的 IP 或域名试用看看吧。

PS: 如果你停止/删除了 Rikka 容器，你上传的照片也会一起被删除。如果你不想这样，请参考下一节：使用数据卷。

### 使用数据卷

Docker 提供了数据卷的功能，这样就不用爬和 Rikka 无关我们上传的图片在应用关闭之后丢失了。

使用方法：

1. 创建数据卷：`docker volume create --name rikkafiles`
2. 在启动 Rikka 容器时加上如下参数：`-v rikkafiles:/go/src/github.com/7sDream/rikka/files`

PS：你可以使用 Rikka `fs` 插件的 `-dir` 参数指定文件储存位置，比如这样：

`docker run -d -P -v rikkafiles:/data --name rikka 7sdream/rikka:latest -pwd 12345 -dir /data`

这样就不用把挂载路径设的太长了。

## 方式 3: 使用 Docker 云服务提供商

比如，我们可以用 DaoCloud 的免费配额来部署一个 Rikka 服务。

详细步骤请看 [DaoCloud 部署教程](https://github.com/7sDream/rikka/wiki/%E5%9C%A8-DaoCloud-%E4%B8%8A%E5%85%8D%E8%B4%B9%E9%83%A8%E7%BD%B2-Rikka)。