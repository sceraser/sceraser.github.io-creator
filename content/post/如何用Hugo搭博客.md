---
title: "如何用Hugo搭博客"
date: 2019-09-12T15:21:31+08:00
draft: false
---
Hugo号称是世界上最快的博客生成器，它使用Go语言，速度碾压使用js的Hexo，越来越多人选择从Hexo迁移到Hugo，我也不例外。那么，如何用Hugo搭建一个个人博客呢？

#### 第一步：安装Hugo（仅针对Winodws用户）
- 在[Hugo下载页面](https://github.com/gohugoio/hugo/releases)下载Hugo压缩包，并且解压到合适位置
- 配置环境变量，在Path中加入Hugo的位置 
![](/image/img1.png)
- 使用以下命令来检测hugo是否安装成功
```
hugo version
```
#### 第二步： 创建博客生成器
- 在一个合适的位置放置博客生成器，使用以下命令
```
hugo new site quickstart
```
- biu~是不是很快就生成好了呢，这就是hugo的特点，非常的快
#### 第三步： 添加一个主题
- 一个好看的博客怎么能少了好看的主题呢，我们使用官方推荐的Ananke主题
```
git init
git submodule add https://github.com/budparr/gohugo-theme-ananke.git themes/ananke
echo 'theme = "ananke"' >> config.toml
```
#### 第四步： 写一篇文章吧
- 让我们开始写文章吧
```
hugo new posts/my-first-post.md
```
- 你可以在posts文件夹中找到它，使用maekdown语法编辑就可以了,记得把draft改成false，因为你不是在写草稿
#### 第五步： 运行服务
- 万事俱备，让我们开始运行吧
```
hugo server -D
```
- 现在你可以在http://localhost:1313/中预览你的博客了