---
title: 博客搬家 - 记第四次搬家(hugo建站推送到谷歌云存储)
date: "2020-04-10"
url: /blog-migration-4/
tags: [博客搬家, hugo, github, github action, google cloud storage, cloudfare]
---

**修订历史**

- 2020.05.19 修订2个错误 - 1. 新域名需要绑定 Google Search; 2. Google Cloud Storage 权限设置。最近新搭建了[敏捷家的博客](https://www.agileplus.co/)，发现了前面的两个错误。
- 2020.04.10 创建

# 写在前面，搬迁记录

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

# 博客的配置 (手把手教你配置)

## 第一步，配置hugo

安装 hugo 可以参考我朋友的博客，[免费搭建一个静态博客](https://github.com/jijiechen/static-blog-manual)。搭建完成后，关于主题，这里我采用的 [hugo](https://gohugo.io/) 主题是 [Ezhil](https://github.com/vividvilla/ezhil)，可以直接用 github fork一份 hugo 主题。具体操作参考 [Ezhil](https://github.com/vividvilla/ezhil)。

hugo和主题都准备好后，目录结构如下：

- content/ 博客的源文件，markdown格式
- public/ 博客的静态网页，hugo自动生成（根据你选择的模板生成漂亮的静态网页）
- static/ 博客的全局静态资源，如全局使用的图片
- theme/ 博客的主题
- config.toml 博客的配置文件

## 第二步，新建github仓库

github上需要创建一个新的仓库 （假设你已经有了github账号）。然后把本地的博客目录中，除了 `public/` 目录的内容推送到代码仓库中。

1. 访问 [github](http://githug.com/)，登录（注册）账号
2. 新建一个仓库，如下图，点击 `New Repository`

![new github repository](/images/github-new-repository.png)

3. 填写仓库的名字，选择仓库的可见性（默认公开的、可以选择私有的），勾选初始化时创建 `README` 文件，如下图：

![create github repository](/images/github-create-repository.png)

下一步需要创建并配置 [谷歌存储 - Google Cloud Storage](https://cloud.google.com/storage)，然后再回来配置 github secrets


## 第三步，google cloud storage

这里我用的谷歌存储，也可以选择国内的阿里云，腾讯云的OSS服务。

[谷歌存储 - Google Cloud Storage](https://cloud.google.com/storage)，需要创建一个存储。
访问 Console 如下图
![google cloud storage console](/images/google-cloud-storage-console.png)

### 3.1 创建存储（bucket）

这里由于我是博客迁移，之前 Google Search 上面已经验证过域名。

**验证域名**

a. 打开 [Google Search](https://search.google.com/search-console)  
b. 点击左上角 `搜索资源` 的小三角，点击`添加资源`  
c. 网域输入你的域名，点击继续  
d. 域名提供商处，增加一条 TXT 记录，值为该页面提供的
e. 一般在几分钟到48小时内生效，耐心等待。点击 `验证` 检查是否生效

![google cloud storage create bucket](/images/google-create-bucket.png)

创建存储，注意：`名字必-须是 www.yourdomain.com` 不能设置为根域名（即这里需要是 CNAME 的名字设置bucket名字）。
根域名可以通过 DNS 的设置来实现。

> 注意存储分区（bucket）名字必须是 CNAME 域名的名字（必须是完全一致），如我的分区名字是 [www.bobjiang.com](www.bobjiang.com)。存储分区不支持直接改名，可以先创建新名字的存储分区，然后把数据转移过去来实现。 

![input bucket name](/images/google-bucket-name.png)

访问权限，可以修改为“统一”方式，这样可以简单操作。
![bucket permission](/images/google-bucket-permission.png)

### 3.2 增加访问权限
下面是为新建的存储分区（bucket）增加访问权限，点击“修改存储分区权限”
![bucket update permission](/images/google-update-permission.png)
点击“添加成员”
![add all Users](/images/google-add-users.png)
输入 新成员：allUsers， 角色：Storage Object Viewer （要严格检查这里的角色权限）
![add roles to allUsers](/images/google-allusers-addroles.png)

最后可以检查一下权限的设置，这里应该提示如下：“在互联网上公开”
![check bucket public](/images/google-storage-public.png)

除了“修改存储分区权限”，还需要“修改网站配置”，增加索引页面后缀为 `index.html` （根据你的实际情况配置）。

### 3.3 权限设置
这里主要设置 服务账号 （service account），为了给其他的第三方进行服务（如接下来我们用 github action 连接）授权。

1. 进入服务账号页面，选择“IAM和管理”，点击“服务账号”，如图

![google service account](/images/google-service-account.png)

2. 点击“创建服务账号”

![google service account](/images/google-create-service-account.png)

3. 输入“服务账号名称”，“服务账号ID”，和“服务账号说明”

![google service account](/images/google-service-account-create-1.png)

4. 第二步默认值即可，进入第三步如下图，点击“创建密钥”

![google service account](/images/service-account-key.png)

5. 选择密钥类型 JSON

![google service account](/images/key-type.png)

6. 密钥生成后，保存到本地（一定保存好密钥，不要丢失）。使用这个密钥和服务账号，就可以访问你的谷歌云存储。

![google service account](/images/store-key.png)

7. 记住服务账号的邮箱，如下图：

![google service account email](/images/service-account-email.png)

下一步配置 github secrets

## 第四步，github secrets

如图创建如下的两个 github secrets：
1. GCP_SA_EMAIL - 值可以参考 服务账号的创建小节
2. GCP_SA_KEY - 值为下面命令的结果（用本地的 JSON 密钥生成，命令如下）

`cat your-json-key.json | base64`

![add github secrets](/images/github-add-secrets.png)

## 第五步，github action

Github action的作用是：
1. 有代码push 或者pull request到仓库时，自动出发下列动作
2. 准备一个 ubuntu 编译环境
3. 准备 hugo 环境
4. 进行 hugo 编译
5. 编译后的 public 目录 （静态网页） 上传到 [谷歌存储 - Google Cloud Storage](https://cloud.google.com/storage)

新建 github action ，并点击 “set up workflow yourself”

![github action](/images/github-action-1.png)
![github action setup your workflow](/images/github-action-setup-your-actions.png)

我的 github action 代码如下：

```
# github action的名字，可以随意改
name: build hugo and deploy to google cloud platform (storage)

# 什么时候调用 action，这里是当 master 上有代码 push 或者 pull request 会触发 github action
on:
  push:
    branches: [ master ]
  pull_request:
    branches: [ master ]

# 环境变量的设置，下面会用到
env:
  GCP_SA_EMAIL: ${{ secrets.GCP_SA_EMAIL }}
  GCP_SA_KEY: ${{ secrets.GCP_SA_KEY }}
  GCP_BUCKET: www.bobjiang.com

# 任务的准备，用 ubuntu最新的环境
jobs:
  setup-deploy:
    name: Setup and Deploy
    runs-on: ubuntu-latest
    steps:

# 检出master分支的代码 checkout
    - name: Checkout
      uses: actions/checkout@v2

# 准备hugo环境
# hugo ready & build
    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: '0.62.2'
        # extended: true

# hugo 编译生成静态网页 public目录内的内容
    - run: hugo --minify

# deploy to google storage
# 准备 连接到 google 云
    - uses: GoogleCloudPlatform/github-actions/setup-gcloud@master
      with:
        version: '285.0.0'
        project_id: ${{ secrets.GCP_PROJECT_ID }}
        service_account_email: ${{ secrets.GCP_SA_EMAIL }}
        service_account_key: ${{ secrets.GCP_SA_KEY }}
        export_default_credentials: true
# 检查 google 云的连接结果
    - run: gcloud info
# 用 gsutil 推送 public 目录内容到谷歌云存储
    - run: gsutil -m rsync -d -c -r public gs://$GCP_BUCKET
    - run: gsutil -m setmeta -h "Cache-Control:public, max-age=3600" gs://$GCP_BUCKET/**/*.html
    - run: gsutil -m setmeta -h "Cache-Control:public, max-age=31536000" gs://$GCP_BUCKET/js/*.js
    - run: gsutil -m setmeta -h "Cache-Control:public, max-age=31536000" gs://$GCP_BUCKET/css/*.css
```

# 总结

经过本次梳理后，写博客完全是本地操作且可以本地调试。
写博客在 hugo 项目的 content 目录内写 markdown 文件
调试可以用 hugo server 本地访问 http://localhost:1313/

效果满意后，可以把 content 目录内的改动 推送到 github 仓库
后面就是自动化准备环境编译、部署（github action）到谷歌云存储。

所以作为一个业余写手，需要更加关注的是内容产出。  
自动化啦……

