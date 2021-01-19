---
Title: 免费发布自己的https ssl证书 | 阿里云收费https服务应对方案
Date: 2021-01-18
URL: /how-to-create-your-https-certificate-free/
description: "阿里云静态网站上如何使用自己的https证书。为自己的二级域名发布免费的https证书。"
tags: [https证书, ssl证书, 免费, 阿里云https]
---

折腾了一天的阿里云OSS静态网站，已经能够成功的部署。部署流水线如下：

本地 -> github -> github action -> 上传阿里云OSS

但是发现阿里云OSS只能为根域名提供免费的https证书，而对于泛域名是不支持免费的https证书。这个对于一个个人博客来讲，还想不牺牲安全性，那么就要想办法了。

自己动手制作 https 证书就变得有必要了。

参考下面的文档：

https://gist.github.com/fntlnz/cf14feb5a46b2eda428e000157447309

核心的命令如下（做个记录）：

```
# 生成根证书私钥
 1253  openssl genrsa -des3 -out rootCA.key 4096
#生成根证书公钥 
 1255  openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 1024 -out rootCA.crt
# 生成网站域名证书私钥 
 1259  openssl genrsa -out bobjiang.com.key 2048
# 生成网站域名证书公钥 
 1260  openssl req -new -key bobjiang.com.key -out bobjiang.com.csr
# 检查网站域名证书 
 1262  openssl req -in bobjiang.com.csr -noout -text
# 生成网站域名证书  
 1263  openssl x509 -req -in bobjiang.com.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out bobjiang.com.crt -days 500 -sha256
# 检查生成的网站https证书 
 1268  openssl x509 -in bobjiang.com.crt -text -noout
 ```