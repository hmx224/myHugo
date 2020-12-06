# myHugo
hugo搭建blog
参考文档：https://www.gohugo.org/

## 生成站点
```cgo

hugo new site /path/to/site

```
## 安装皮肤


```cgo

cd themes
git clone https://github.com/flysnow-org/maupassant-hugo
git clone https://github.com/pagecho/maupassant.git
git clone https://github.com/spf13/hyde.git

```
## 创建文档

```cgo

hugo new post/xxx.md


```
## 运行Hugo

```cgo

hugo server --theme=maupassant-hugo --buildDrafts

```

## 在线浏览器访问
[在线博客](https://www.ifanatic.cn)

## 本地访问 
http://localhost:1313/

## 部署

```cgo

hugo --theme=maupassant-hugo --baseUrl="http://hmx224.github.io/"

```

## 配置webhook

webhook是GitHub上提供的Git的一种Hook机制，当代码发生变化时，比如代码被Push到GitHub的Repo时，GitHub会自动请求一个你指定的网页，
并且把变更相关的参数都传递过来。入口在Repo的Settings - webhooks & services

说明文档：https://developer.github.com/webhooks/

借助webhook的机制，我们就可实现当有新的文章Push之后，自动通知远程的一台机器执行一个脚本，脚本的内容就是生成静态页面和Push部署到最终的服务器。

webhook的Server接收webhook通知，然后执行一个脚本。这样的需求太普遍了，以至于完全不需要自己来实现。在GitHub里搜webhook可以搜出来很多。
我主要挑选了Go语言的版本。主要有两个：

https://github.com/qiniu/webhook
https://github.com/adnanh/webhook

第一个是七牛写的，代码很简单，用法也很简单。开始打算用七牛的版本。最后调试的时候发现json解析失败，完全不可用啊！有点坑爹。
于是换成了第二个，这个Repo有200多个Star。还是靠谱很多，最后部署，调试，非常顺利。


```
go get github.com/adnanh/webhook
```

写一个配置文件hooks.json，里面指定需要执行的脚本：

```
[
  {
    "id": "redeploy-webhook",
    "execute-command": "/var/scripts/redeploy.sh",
    "command-working-directory": "/var/webhook"
  }
]
```
指定端口启动：
```
$ /path/to/webhook -hooks hooks.json -port=9876 -verbose
```

然后它将接受webhook地址：（把它填到GitHub里的webhook里）
```
http://yourserver:9876/hooks/redeploy-webhook
```
## 自动部署
