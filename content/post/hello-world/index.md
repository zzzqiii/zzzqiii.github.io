---
title: 使用hugo stack主题创建博客
description: Welcome to Hugo Theme Stack
slug: hello-world
date: 2023-02-11 00:00:00+0000
image: cover.jpg
categories:
    - 学习
tags:
    - hugo
---

之前换了电脑后懒得折腾，写的博客差不多一年没更新了，今天终于恢复好了，以前写的文章太乱了，所以这次干脆重建好了。还是用之前的hugo主题[hugo-theme-stack](https://github.com/CaiJimmy/hugo-theme-stack)，现在这个版本可以不用下载主题，自动部署在GitHub上[
hugo-theme-stack-starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)。虽然简单了很多，但还是踩了很多坑，记录一下。



#### 安装

1. 安装hugo

用管理员打开powershell，安装choco，用choco安装hugo

```powershell
Set-ExecutionPolicy RemoteSigned

Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

choco install hugo-extended
```

2. 安装go

下载安装包https://golang.google.cn/dl/，安装。



#### 部署

1. 修改GitHub默认分支

先将github新建的repository的默认分支设置修改为master，Setting=》Repository=》main修改为master。

2. 创建GitHub repository

以[hugo-theme-stack-starter](https://github.com/CaiJimmy/hugo-theme-stack-starter)模板创建仓库，点击Use this template，

新建repository，设置名字为username.github.io。后缀要加上.github.io，否则无法访问http://username.github.io

3. 修改action的设置

Settings=>Actions=>General=>Workflow permissions选择read and write permissions.

4. 将Github上新建的hugo-theme-stack-starter仓库关联到本地

```bash
git clone git@github.com:zzzqiii/zzzqiii.github.io.git
```

5. 设置GitHub Pages

Settings=>Pages=>Build and deployment=>Branch，选择gh-pages，save。

6. 在本地下载主题

在主目录下新建themes文件夹，下载主题

```bash
git clone git@github.com:CaiJimmy/hugo-theme-stack.git
```





#### 修改配置

修改config\\_default中的配置文件。包括：

1. **修改config.toml文件**

- 修改baseurl、语言、主题

```
# Change baseurl before deploy
baseurl = "https://zzzqiii.github.io/"
languageCode = "zh-cn"
paginate = 5
title = "Every day counts"
theme = "hugo-theme-stack"

# Theme i18n support
# Available values: en, fr, id, ja, ko, pt-br, zh-cn, zh-tw, es, de, nl, it, th, el, uk, ar
DefaultContentLanguage = "zh-cn"

# Set hasCJKLanguage to true if DefaultContentLanguage is in [zh-cn ja ko]
# This will make .Summary and .WordCount behave correctly for CJK languages.
hasCJKLanguage = true

# Change it to your Disqus shortname before using
#disqusShortname = ""
```

- 谷歌搜索

打开谷歌搜索site:https://zzzqiii.github.io/。如何搜不到说明未被收录，为了让网站能被搜到，登录[谷歌分析](https://analytics.google.com/analytics/web/provision/#/provision)，账号开设=》媒体资源设置=》关于您的商家=》选择平台（网站）=》输入网址=》复制网站数据流的衡量ID。

在config.toml中写入衡量ID，将网址与google analytics关联。

```
# GA Tracking ID
googleAnalytics = "G-*****"
```



2. **修改params.toml文件中的参数**

- 设置网站图标

在主目录下新建static文件夹，把favicon.ico文件放在static文件夹中。在params.toml中新增：

```
favicon = "/favicon.ico"
```

- 修改emoji

在[📙 Emojipedia — 😃 Home of Emoji Meanings 💁👌🎍😍](https://emojipedia.org/) 上复制想要的标签

- 设置头像

在主目录下新建assets/img文件夹，把头像avatar.jpg放在img文件夹中，

```
[sidebar.avatar]
enabled = true
local = true
src = "img/avatar.jpg"
```

- 修改评论系统

这里使用utterances评论系统，要先将utterances和GitHub关联，访问[utterances](https://github.com/apps/utterances) 点击install，然后修改配置文件params.toml

```
[comments]
enabled = true
provider = "utterances"

[comments.utterances]
repo = "zzzqiii/zzzqiii.github.io"
issueTerm = "pathname"
label = ""
```



通过hugo new post/title/index.md新建文章，文件名为index.md，否则无法显示同文件夹下的图片作为头图。

完成修改后push到github上

```bash
git status
git add .
git commit -m "update"
git push -u origin master
```

执行git push时，github会自动运行workflow进行部署，如果前面不修改action权限，这里会报错。

部署好了后会发现actions这里执行好了两个workflows：update和pages build and deployment.

并且在master下面新增了一个分支：gh-pages。

最后，访问user.github.io即为作者设置好的默认主页，通过hugo命令可以新增文章。



参考：

https://stack.jimmycai.com/

https://blog.tuwei.space/p/%E8%AE%B0%E5%BD%95%E6%90%AD%E5%BB%BAhugo-%E5%8D%9A%E5%AE%A2%E4%BD%BF%E7%94%A8stack%E4%B8%BB%E9%A2%98%E5%BF%AB%E9%80%9F%E5%90%AF%E5%8A%A8%E9%83%A8%E7%BD%B2/

https://huohuade-blog.github.io/p/%E7%94%A8hugo-stack%E4%B8%BB%E9%A2%98%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E4%B8%BB%E9%A1%B5/



