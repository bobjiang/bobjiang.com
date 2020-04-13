---
Title: 如何用google cloud存储分区搭建网站 个人博客
Date: 2019-12-27
URL: /how-to-build-website-host-google-cloud/
tags: [host website, google cloud, blog]
---

## Step 1
注册 google cloud - https://cloud.google.com/?hl=zh-cn
1.1 所在地随意选择，我选择新加坡，填写正确的信用卡，选择个人
激活后获得一年的免费使用（300美元或365天，先用完就结束免费期）

## Step 2
准备验证域名
3.1 自己有域名，如我的域名是 bobjiang.com
3.2 验证你是否拥有该域名，打开 [search console](https://search.google.com/search-console?hl=zh-cn)
3.3 点开左上角下拉的小三角，选择添加资源
3.4 网域（domain）输入自己的跟域名，如 bobjiang.com ， 点击继续
3.5 到域名注册商的管理页面（我用的 godaddy.com），找到自己域名的DNS管理
3.6 增加一条DNS解析记录， 类型 TXT，值复制页面上 google提供的内容
3.7 点击验证，如果验证不通过需要多等一下，最多等1天

## Step 3
准备域名指向
4.1 到域名注册商的管理页面（我用的 godaddy.com），找到自己域名的DNS管理
4.2 增加一条DNS解析记录， 类型 CNAME，值 www， 指向 c.storage.googleapis.com.

## Step 4
创建google存储分区
5.1 [进入项目选择器页面](https://console.cloud.google.com/projectselector2/home/dashboard)
5.2 选择一个你拥有的域名，如上述我的 bobjiang.com
5.3 创建新的存储分区，名字是 www.bobjiang.com （一定是这个名字!!! 和你的CNAME一致）

## Step 5
上传文件并修改权限
6.1 用控制台上传文件，如打开 [cloud storage 浏览器](https://console.cloud.google.com/storage/browser)
6.2 点击创建的存储分区的名字
6.3 点击上传文件按钮
6.4 选择一个本地文件上传
6.5 上传后需要修改权限，点击`权限`标签页
6.6 点击添加成员按钮。
6.7 随即会显示“添加成员”对话框。
6.8 在新成员字段中，输入 allUsers。
6.9 在角色下拉列表中，选择存储空间子菜单，然后点击 Storage Object Viewer 选项。点击保存。

## Step 6
测试验收
访问 [bobjiang.com/me](https://bobjiang.com/me) 验收

