# Coffee
一个极简的高性能 HTTP/HTTPS 服务器，所有请求都会返回 418 I'm a teapot\
该项目追求 轻量化、小体积、高性能，适合作为占位服务或测试用途\
可以实现用茶壶煮咖啡的错误输出

## 特性
同时监听 80（HTTP） 和 443（HTTPS）\
内嵌 TLS 证书，无需额外配置

所有请求统一返回：
```
HTTP/1.1 418 I'm a teapot
Content-Length: 0
Cache-Control: public, max-age=315360000, immutable
```

CDN / 浏览器可缓存 10 年
不解析 HTTP 请求\
极高 QPS\
静态编译 Go 二进制\
程序体积小于 10KB（含占很大部分空间的内嵌证书）\
无任何依赖

## 使用场景
占位源站（Placeholder Origin）\
RFC2324（I'm a teapot）相关测试

## 性能
由于该服务器：\
不解析 HTTP\
不进行复杂处理\
仅执行一次写入操作\
在即使 1核/512M (不超开) 的情况下上可以有几万 QPS 的处理能力\

## 编译
```
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 \
go build -trimpath -ldflags "-s -w" -o coffee
```
可选压缩：
```
upx --lzma coffee
```
运行
```
sudo ./coffee
```

监听端口：\
80 (HTTP), 443 (HTTPS)

## 许可证
不要求保留版权，可以闭源，可以倒卖，可以原封不动拿去就说是你写的\
当然一切的前提条件是用出了事别要我担责就行
