---

title: "Laravel55博客项目说明xblog"
date: 2020-12-07T15:25:27+08:00
draft: false
toc: true
tags: ["Laravel"]
categories: ["Laravel"]
---

[toc]

# 文档地址

> https://xblog.lufficc.com/blog/how-to-install-my-blog

## 环境要求

安装npm install过程会存在问题，以下的版本可以运行成功
npm版本 6.14.4
node版本 v10.21.0
composer 2.0.7



```
{
  "private": true,
  "scripts": {
    "dev": "npm run development",
    "development": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "watch": "cross-env NODE_ENV=development node_modules/webpack/bin/webpack.js --watch --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js",
    "watch-poll": "npm run watch -- --watch-poll",
    "hot": "cross-env NODE_ENV=development node_modules/webpack-dev-server/bin/webpack-dev-server.js --inline --hot --config=node_modules/laravel-mix/setup/webpack.config.js",
    "prod": "npm run production",
    "production": "cross-env NODE_ENV=production node_modules/webpack/bin/webpack.js --progress --hide-modules --config=node_modules/laravel-mix/setup/webpack.config.js"
  },
  "devDependencies": {
    "autosize": "^4.0.2",
    "bootstrap": "^4.1.1",
    "chart.js": "^2.7.2",
    "clipboard": "^1.7.1",
    "cross-env": "^5.1.6",
    "font-awesome": "^4.7.0",
    "highlight.js": "^9.12.0",
    "jquery": "^3.2",
    "jquery-bridget": "^2.0.1",
    "laravel-mix": "^1.0",
    "magnific-popup": "^1.1.0",
    "masonry-layout": "^4.2.0",
    "node-sass": "^4.9.0",
    "popper.js": "^1.14.3",
    "simplemde": "^1.11.2",
    "smooth-scroll": "^14.2.0",
    "uppy": "^0.24.2"
  },
  "dependencies": {
    "ajv-keywords": "^3.4.0",
    "npm": "^6.1.0"
  }
}
```


```
PHP >= 7.0.0
OpenSSL PHP Extension
PDO PHP Extension
Mbstring PHP Extension
Tokenizer PHP Extension
XML PHP Extension
同时，还需要安装好 Composer 和 Node.js® 。
```
## 安装

从 GitHub 下载：
```
git clone https://github.com/lufficc/Xblog.git blog --depth 1
cd blog
```
安装：
```
composer install
cp .env.example .env
php artisan key:generate
```
在.env文件中填好数据库连接，例如：
```
DB_CONNECTION="mysql"
DB_HOST="127.0.0.1"
DB_PORT=3306
DB_DATABASE=blog
DB_USERNAME=root
DB_PASSWORD=123456
```
运行数据库迁移：
```
php artisan migrate
```
安装前端框架：
```
npm install
```
编译前端：
```
npm run dev # 开发模式, 不会压缩 js 和 css, 因此速度很快.
npm run prod # 生产模式, 会压缩 js 和 css.
```

至此，全部安装完毕，你可以启动服务器来访问 http://127.0.0.1:8000：

```
php artisan serve
```

默认情况下，用户 id 为 1 的为管理员，因此首先进入 http://127.0.0.1:8000/register 注册一个用户作为管理员（只有管理员可以写作、进入后台）。

为了不让网站看起来空荡荡的，你可以生产一些假数据：

```
php artisan db:seed
```
到这一步，网站大概看起来就是这个样子了（没有其他任何个性化设置）：
![首页](/images/laravel55博客项目说明xblog/1.png)

## Features

### 文章方面

支持 Markdown, 编辑器支持粘贴板、拖拽上传图片，全屏写作模式, 实时预览, 快捷键, 自动保存。
![编辑器](/images/laravel55博客项目说明xblog/2.png)

文章的多状态管理(发布,撤回,软删除,永久删除,恢复,草稿)
![文章的多状态管理](/images/laravel55博客项目说明xblog/3.png)


单篇文章支持修改评论类型（原生、Disqus），支持关闭、禁止或不显示评论，支持关闭或者显示目录（TOC）。
![文章个性化](/images/laravel55博客项目说明xblog/4.png)

### 评论系统
支持原生自带、Disqus评论系统。支持全站关闭评论， 文章(或者页面)关闭评论，为某一篇文章(或者页面)关闭评论，强制开启评论。
原生自带评论登录未登录均可评论，但是需要管理员审核后才会显示在前端界面。

自带多层级评论系统

以及评论管理系统：
评论管理系统
评论管理系统

评论邮件提醒功能：
邮件提醒
邮件提醒

### Block IP
会记录访问你博客用户的 IP，可以禁止某一 IP 访问你的博客。

Block IP
### 分类, 多标签
每个文章须有一个分类，可以有0个或多个标签。

分类
分类
标签
标签
### 后台管理
后台界面。

后台管理
后台管理
### 图片管理
图片集中管理、上传。

图片管理
图片管理
### 赞赏功能
赞赏功能，可关闭，赞赏语可配置。

## 写作

Xblog 采用 Markdown 格式来存储文章。Markdown 简洁、高效，很容易上手。

### 快捷键
编辑器采用 sparksuite/simplemde-markdown-editor ，支持 SimpleMDE 支持的所有快捷键，同时文章会自动保存在本地，
防止关闭网页导致内容丢失。
```cgo
快捷键	动作
Cmd-'	"toggleBlockquote"
Cmd-B	"toggleBold"
Cmd-E	"cleanBlock"
Cmd-H	"toggleHeadingSmaller"
Cmd-I	"toggleItalic"
Cmd-K	"drawLink"
Cmd-L	"toggleUnorderedList"
Cmd-P	"togglePreview"
Cmd-Alt-C	"toggleCodeBlock"
Cmd-Alt-I	"drawImage"
Cmd-Alt-L	"toggleOrderedList"
Shift-Cmd-H	"toggleHeadingBigger"
F9	"toggleSideBySide"
F11	"toggleFullScreen"
```

### 上传图片
扩展了 SimpleMDE，你可直接拖拽图片到编辑器或者直接将粘贴板的图片粘贴到编辑器，编辑器可以自动上传图片，
并将图片链接以 Markdown 的方式插入到当前光标位置。

```
![filename](image_url)
图题
你可以给图片添加 figure 类让其显示题图，因为采用了 Markdown Extra ，因此在图片链接后面添加{.figure}即可，效果如下图所示。

![这是一个图题](image_url){.figure}
这是一个图题
这是一个图题
画廊
你可以点击编辑器画廊按钮来插入画廊，会插入如下代码：

画廊按钮
画廊按钮
<div markdown="1" class="figure third" caption="画廊标题">
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
</div>
然后可以在中间插入图片。另外，除了三列画廊，还支持两列、四列、五列画廊，只需要分别把 third 类改为half、fourth、fifth即可。其展示效果如下图：

两列画廊
<div markdown="1" class="figure half" caption="两列画廊">
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
</div>
alt
alt
alt
alt
两列画廊
三列画廊
<div markdown="1" class="figure third" caption="三列画廊">
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
</div>
三列画廊
四列画廊
<div markdown="1" class="figure fourth" caption="四列画廊">
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
</div>
四列画廊
五列画廊
<div markdown="1" class="figure fifth" caption="五列画廊">
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
![alt](image_url)
</div>
五列画廊
同时，这些画廊全都是响应式的，在移动设备上会显示为单列。如果 caption 为空的话，画廊图题会设置为所有图片的 alt 中不为空的第一个。
```
### 提示信息
点击编辑器的提示按钮，来插入提示。
```
提示按钮

<div markdown="1" class="alert alert-info">

</div>
例如：

<div markdown="1" class="alert alert-info">
**NOTE:** 我是海贼迷，点击[这里](http://comic.lufficc.com/)看漫画。
</div>
<div markdown="1" class="alert alert-success">
**NOTE:** 我是海贼迷，点击[这里](http://comic.lufficc.com/)看漫画。
</div>
<div markdown="1" class="alert alert-danger">
**NOTE:** 我不是海贼迷，不要点击[这里](http://comic.lufficc.com/)看漫画。
</div>
<div markdown="1" class="alert alert-warning">
**NOTE:** 我是海贼迷，点击[这里](http://comic.lufficc.com/)看漫画。
</div>
<div markdown="1" class="alert alert-dark">
**NOTE:** 我是海贼迷，点击[这里](http://comic.lufficc.com/)看漫画。
</div>
NOTE: 我是海贼迷，点击这里看漫画。

NOTE: 我是海贼迷，点击这里看漫画。

NOTE: 我不是海贼迷，不要点击这里看漫画。

NOTE: 我是海贼迷，点击这里看漫画。

NOTE: 我是海贼迷，点击这里看漫画。
```

### Markdown Extra
Xblog 支持 php Markdown Extra，例如：
```
Markdown Inside HTML Blocks
<div markdown="1">
<div markdown="1"> This is *true* **markdown** text. </div> 
</div>
This is true markdown text.

Footnotes
这个效果的实现具体原理参见原理[^1]。
[^1]: 这是原理1。
这个效果的实现具体原理参见原理1。

Abbreviations
The HTML specification is maintained by the W3C.
*[HTML]: Hyper Text Markup Language
*[W3C]:  World Wide Web Consortium
The HTML specification is maintained by the W3C.

更多效果可以查看 php Markdown Extra。
```

### 数学公式
数学公式采用 MathJax，使用 $ 包裹行内元素，$$ 包裹块元素即可，例如：
```
When $a \ne 0$, there are two solutions to \(ax^2 + bx + c = 0\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$
```

When a≠0, there are two solutions to (ax^2 + bx + c = 0) and they are
x=−b±b2−4ac−−−−−−−√2a.

## 图床（File Storage）

Xblog 默认支持本地、七牛云、Amazon S3、Dropbox 等图床。并且图片与图床独立，你可以随便随时修改图床配置，而不影响图片（文件）的删除等功能，修改 .env 的 DISK 属性只会影响当前上传图片（文件）的位置，因为图片（文件）信息也存储了图床信息到数据库。

### 本地
使用本地图床，只需要将修改.env中 的 DISK=local 或者 DISK=public 即可。
```
public
修改 .env中 的 DISK=public，此时上传文件会存储到 storage/app/public 文件夹，为了使前端可见，需要创建一个链接，从public/storage 到 storage/app/public，运行

php artisan storage:link
即可。

local
修改 .env 中 的 DISK=local，此时上传文件会存储到 storage/app 文件夹，为了使前端可见，需要创建一个链接，从public/storage 到 storage/app，运行

ln -s <project_root>/storage/app <project_root>/public/storage
即可。
```
### 七牛云
修改 .env 中 的 DISK=qiniu，同时填写七牛云相关信息即可。
```
DISK=qiniu
QINIU_AK=
QINIU_SK=
QINIU_BUCKET=
QINIU_DOMAIN= # 结尾不带 ‘/’
```
### Amazon S3
首先需要安装依赖，composer require league/flysystem-aws-s3-v3 ~1.0，然后修改 .env 中 的 DISK=s3，同时填写 Amazon S3 相关信息即可。
```
DISK=s3
S3_KEY=
S3_SECRET=
S3_REGION=
S3_BUCKET=
```
### Dropbox
首先需要安装依赖，composer require spatie/flysystem-dropbox，然后将App\Providers\DropboxServiceProvider::class 添加到 config/app.php 的providers数组，最后修改 .env 中 的 DISK=dropbox，同时填写 Dropbox 相关信息即可。如何生成 access token？看这里。
```
DISK=dropbox
DROPBOX_ACCESS_TOKEN=
```
### 其他图床

参考官方文档 [File Storage](https://laravel.com/docs/5.5/filesystem)，然后在 .env 中填写相关信息即可，无需其他多余改动。

## 缓存
Xblog 支持使用 Redis 来加速你的博客，默认是没有使用缓存的。如果想使用，首先安装 Redis:
```
sudo apt-get install redis-server
```
然后在 .env 中设置 CACHE_ENABLE='true' 即可。

## 个性化
### 首页
首页动态墙纸，在 Settings > 图片 > Home背景图片里面填写，每行为一个图片链接。然后首页会随机循环播放这些图片。
Logo 在 Settings > 网站 > Logo 设置，可以为纯文本或者 HTML。例如 Bootstrap Logo 的 SVG:
```
<svg class="d-block" width="36" height="36" viewBox="0 0 612 612" xmlns="http://www.w3.org/2000/svg" focusable="false">
   <title>Bootstrap</title>
   <path fill="currentColor" d="M510 8a94.3 94.3 0 0 1 94 94v408a94.3 94.3 0 0 1-94 94H102a94.3 94.3 0 0 1-94-94V102a94.3 94.3 0 0 1 94-94h408m0-8H102C45.9 0 0 45.9 0 102v408c0 56.1 45.9 102 102 102h408c56.1 0 102-45.9 102-102V102C612 45.9 566.1 0 510 0z"></path>
   <path fill="currentColor" d="M196.77 471.5V154.43h124.15c54.27 0 91 31.64 91 79.1 0 33-24.17 63.72-54.71 69.21v1.76c43.07 5.49 70.75 35.82 70.75 78 0 55.81-40 89-107.45 89zm39.55-180.4h63.28c46.8 0 72.29-18.68 72.29-53 0-31.42-21.53-48.78-60-48.78h-75.57zm78.22 145.46c47.68 0 72.73-19.34 72.73-56s-25.93-55.37-76.46-55.37h-74.49v111.4z"></path>
</svg>
```
其效果为：

### Header 图片
在 Settings > 网站 > Header背景图片 设置，可以设置一个固定图片地址，也可以设置为动态更新的，如何必应搜索每日壁纸保持同步，或者定期随机从 Picsum 选择一张图片。

你如果使用了动态更新，需要在服务器添加配置，运行 crontab -e ,然后添加
```
* * * * * php /path-to-your-project/artisan schedule:run >> /dev/null 2>&1
```

即可，详见 [Task Scheduling](https://laravel.com/docs/5.5/scheduling) 官方文档。

Header 展示
Header 展示
设置 Header 图片
设置 Header 图片

### 个人信息
在 Settings > 个人信息 设置你的头像、用户名、社交链接等信息，会显示在首页和博客右边栏。同时，其他信息 栏可以为 HTML，其最终会拼接到博客右边栏（博客右边栏实际为 Bootstrap 的一个 card，因此自定义 HTML 最好用 card-body 类包裹，来获取相同 pad。），如设置为 DigitalOcean 的邀请链接：
```
<div class="card-body border-top"> 
<div class="media">
<a  class="align-self-center d-flex mr-3" href="https://m.do.co/c/fd4deae8d4f4" target="_blank">
<svg xmlns="http://www.w3.org/2000/svg" width="50" height="50" viewBox="0 0 50 50"><title>DigitalOcean</title><g fill="#0080FF" fill-rule="evenodd"><path d="M24.9153 50v-9.661c10.226 0 18.1638-10.1413 14.2372-20.904-1.4406-3.983-4.6327-7.1751-8.6158-8.6158C19.774 6.921 9.6327 14.8305 9.6327 25.0565H0C0 8.7571 15.7627-3.9548 32.8531 1.3842c7.4576 2.3446 13.418 8.2768 15.7345 15.7344C53.9266 34.2373 41.2429 50 24.9153 50"></path><path d="M15.339 40.3672h9.6045v-9.6045H15.339zM7.9379 47.7684h7.401v-7.4012H7.938zM1.7514 40.3672H7.938v-6.1864H1.7514z"></path></g></svg>
  </a>
  <div class="media-body">
<p class="card-text">Easily deploy an SSD cloud server on DigitalOcean in 55 seconds. Sign up using my link and receive $10 in credit.</p>   
  </div>
</div>
</div>
```
其效果为：

### 其他
还有很多其他个性化设置，如每页数量、热门文章数量、备案号、赞赏描述等等，就不一一详细介绍了，在后台很容易就看到啦。
```
<p>这是原理1。&#160;<a href="#fnref1:1" rev="footnote" class="footnote-backref">&#8617;</a></p>

```

写的不错，帮助到了您，赞助一下主机费~
