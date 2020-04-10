---
title: 博客搬家 - 记第四次搬家(hugo建站推送到谷歌云存储)
date: "2020-04-10"
url: /blog-migration-4/
tags: [博客搬家, hugo, github, github action, google cloud storage, cloudfare]
---

记录我的博客这次搬家过程。我的博客之前经历过：

1. wordpress
2. github page
3. [Bitcron](https://bitcron.com/) - 机制很不错（写完的博客自动保存到dropbox并发布，可惜搜索引擎的收录不是很好。）
4. 这次搬迁 2020年4月10日 初步完成

# 博客的架构

现在写博客一直采用 `markdown` 语法，所以也是本次可以顺利迁移的一大前提。
最近两年一直用的是 [Bitcron](https://bitcron.com/) ，非常顺滑。每次写完 md 文件，直接保存即可（博客立即更新可见）。不过一直搜索引擎的收录不是很好，如我直接搜索 "Bob Jiang" 我的博客始终排不到第一个。很奇怪……

索性现在申请了一年免费的 google cloud，就做个搬迁。

搬迁之后的博客存储在 [google cloud storage](https://cloud.google.com/storage) 上，DNS也顺便切换到 [Cloudfare](https://cloudflare.com) 上了。
博客系统使用的是 [hugo](https://gohugo.io/) ，主题用的是 [Ezhil](https://github.com/vividvilla/ezhil)。博客整体存放于 github上，每次提交到github会自动出发一次 github action，推送到谷歌存储。

# 博客的工作流

博客的工作机制如下：

1. 本次编写博客(md文件) 并本次检查 (`hugo server`)
2. github push 到 github 仓库
3. 每次 push 或者 pull request 会出发 github action
4. github action 进行 [hugo](https://gohugo.io/) 编译
5. github action 推送博客静态文件到 [谷歌存储](https://cloud.google.com/storage)

# 博客的配置

## hugo

## github

### github security

### github action

## google cloud storage

### 创建存储（bucket）

### 权限设置

# 总结
