---
Title: 网站地图之搜索引擎收录
Date: 2019-04-24
URL: /sitemap-google/ 
tags: [sitemap, google]
---

# 网站地图之搜索引擎收录

无意中发现我的博客从2015年起，并不在谷歌搜索引擎的收录中。即你在谷歌是查不到我的博客内容的。

既然发现问题，就要定位问题出在哪儿，以及修复它。

## 定位问题
使用[google search console](https://search.google.com/search-console)，把网站加进去。

需要网站的DNS域名增加一条TXT记录，用来确认你是网站的站长。

确认后，检查网站链接的有效性。如下图，点击“网址检查”  
![](/_image/link-inspection.png)

输入你网站中的任何网址，如可以输入 `bobjiang.com` (BoB的博客)

检查报告如下：  
![](/_image/site-report.png)

我的博客还未完全恢复，显示Google仍未收录。

这里根据报告，就可以找到详细的问题描述，以及更多帮助信息。

我的网站提示为被 `robots.txt` 禁止抓取。

## 解决问题
既然被 `robots.txt` 禁止抓取，检查网站博客中的所有文件后未发现 robots.txt 。

咨询博客提供商（海波同学），发现有一处关键设置，即是否允许机器人设置为 yes。修改为 no 后即可。

为了更快恢复所有的抓取，需要生成网站地图。

这里有谷歌推荐的第三方网站地图生成工具列表[1].

有5类：  
- 可部署的服务器端程序
- 内容管理系统（CMS）插件，如大名鼎鼎的 wordpress
- 可下载的工具（如windows，Mac系统的）
- 在线服务
- 自带网站地图的CMS系统

我选择了在线服务（不用部署、不用下载，但可能有一定的限制）：

[XML sitemap generator](https://xmlsitemapgenerator.org/)

### 生成网站地图
1. 填写对应的网站信息，如图：  
![](/_image/generate-sitemap.png)

2. 点击按钮 `Generate sitemap`
3. 生成后，点击下载 sitemap XML file
4. 上传sitemap.xml文件到网站目录，如我的上传在网站根目录：

> https://bobjiang.com/sitemap.xml

5. 返回 google search console
6. 点击左侧导航栏的 `索引 - 站点地图`，结果如下图：  
![](/_image/sitemap-google.png)

上图结果显示我的网站上次被谷歌收录的时间是2015年12月9日。

7. 输入站点地图的网址，如 https://bobjiang.com/sitemap.xml  
提示：可以用浏览器检测一下输入是否正确。

至此，问题修复。

大概需要等一段时间(最多48小时)，等谷歌重新开始抓取。

## 参考资料
[1] [谷歌推荐的三方的网站地图生成器](https://code.google.com/archive/p/sitemap-generators/wikis/SitemapGenerators.wiki) 
[2] [XML sitemap generator](https://xmlsitemapgenerator.org/)

# 思考
通过这次的问题，我发现博客还是要维护的，尤其是定期用搜索引擎自己检查一下。

## 每日问题
- 有没有什么事情对你很重要，但你并没有定期检查呢？

## 关于作者
**BoB Jiang**

- 中国北方的第一位CST（Certified Scrum Trainer）  
- [敏捷变革中心](https://www.c4at.cn/)（Center for Agile Transformation）合伙人  
- [Bob的博客](https://www.bobjiang.com)、《Scrum精髓》译者
- 欢迎加入`自由职业者俱乐部` 微信群，请加微信：
- hiblocknet  ； 添加微信后，发送消息 `dream`

## 版权声明

本文采用 [CC BY-NC-SA 3.0 许可协议](https://creativecommons.org/licenses/by-nc-sa/3.0/deed.zh)。  
转载请注明出处！
