# myHugo
hugo搭建blog

## 安装皮肤

```cgo

cd themes
git clone https://github.com/flysnow-org/maupassant-hugo

```
## 运行Hugo

```cgo

hugo server --theme=maupassant-hugo --buildDrafts

```

## 浏览器访问
[访问](localhost:1313)

## 部署

```cgo

hugo --theme=maupassant-hugo --baseUrl="http://hmx224.github.io/"

```