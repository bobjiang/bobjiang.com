---
title: "Ruby On Rails 学习笔记（1）"
date: "2013-12-11"
---

**1\. 第一步是搭建环境** 笔者的环境是win7,上网搜索发现一个非常好的网站[http://railsinstaller.org](http://railsinstaller.org "http://railsinstaller.org"),直接下载最新版,已经包含：

- ruby
- rails
- bundler
- git
- sqlite
- tinyTDS
- sqlserver\_support
- devkit

**2\. 第一个项目** rails里新建项目非常简单，使用命令`rails new ...`即可。下面是笔者的实例，项目名称是pl [![ror](/wp-content/uploads/2013/12/ror-300x196.png)](/wp-content/uploads/2013/12/ror.png) 项目新建成功后的目录和文件如下： _目录_ app - MVC框架的主要目录，大部分的开发工作在这里完成。对应MVC模式，分别有3个目录（models,views,controllers）；assets存放图片，JS和CSS config - 配置rails运行时的规则、路由和数据库等 db - 数据库 doc - 说明文档 lib - 库文件 log - 日志 public - 通过WEB可见的部分，包括静态文件和编译后的css,js test - 单元测试，fixtures tmp - 临时目录，存放临时文件 vendor - 第三方代码 _文件：_ config.ru - Rack配置 Gemfile - 指定rails的依赖，Bundler使用这个配置文件 Gemfile.lock - 同上 Rakefile - 查找和加载任务，可以在命令行使用（rake ...）；如果要添加任务，可以放在lib/tasks目录内 README.rdoc - 应用的介绍
