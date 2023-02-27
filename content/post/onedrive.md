---
title: OneDrive设置自动同步
date: 2023-02-27T18:03:45+08:00
draft: true
image: img/onedrive-logo-chmura-microsoft.jpg
categories:
    - 学习
tags:
    - OneDrive
---

最近发现用学校的邮箱登录OneDrive有5T的空间，https://www.microsoft.com/zh-cn/education/products/office，果断白嫖，登录之后就可以在电脑上备份文件。注意在电脑上登录的时候会提示要不要把文档桌面等等文件夹同步过去，可以先跳过。

添加文件的方法是：

> 第一步是向您的 OneDrive 添加文件。 从 PC 或 Mac 添加文件的最佳方式是下载 OneDrive 并将文件 拖入 OneDrive 文件夹。 假定您在笔记本电脑上创建了一个 PowerPoint 演示文稿 — 您可以将其拖入 您的 OneDrive 文件夹，以便从您的手机访问该文件。

移动或复制到OneDrive文件夹就好了。

但是这样原文件修改后不会同步，要在OneDrive文件夹里的文件修改才会同步。不像坚果云一样，右键点击同步改文件夹之后就可以同步到云端了。

OneDrive同步的方法是创建软连接：

`mklink /d "onedrive文件夹地址\需要同步的文件夹名" "需要同步的文件夹地址"`

例如我要同步E盘中的doc文件夹到onedrive中的E盘备份文件夹：

先在OneDrive中新建E盘备份文件夹，然后创建软连接

`mklink /d "D:\OneDrive\OneDrive - zju.edu.cn\E盘备份\doc" "E:\doc"`

这样就会在onedrive中的E盘备份文件夹中自动新建doc文件夹并把里面的东西同步。

注意不要提前在OneDrive中创建需要同步的文件夹名，否则会报错：当文件已存在时，无法创建该文件。
