---
Title: 免费发布自己的https ssl证书 | 阿里云收费https服务应对方案
Date: 2021-01-18
URL: /how-to-create-your-https-certificate-free/
tags: [https证书, ssl证书, 免费, 阿里云https]
---

折腾了一天的阿里云OSS静态网站，已经能够成功的部署。部署流水线如下：

本地 -> github -> github action -> 上传阿里云OSS

但是发现阿里云OSS只能为根域名提供免费的https证书，而对于泛域名是不支持免费的https证书。这个对于一个个人博客来讲，还想不牺牲安全性，那么就要想办法了。

自己动手制作 https 证书就变得有必要了。

参考下面的文档：

https://gist.github.com/fntlnz/cf14feb5a46b2eda428e000157447309