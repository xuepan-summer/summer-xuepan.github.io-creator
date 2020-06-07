---
title: "Hugo搭建个人博客"
date: 2020-06-07T14:39:18+08:00
draft: false
---

1.安装hugo

Windows:
+ 下载windows相应版本的压缩包（对应32位/64位）并解压
+ 将hugo.exe放到D:\softwares\hugo\hugo.exe
+ 将D:\softwares\hugo加到PATH中
+ 重启终端，运行hugo version查看版本验证安装成功
  
Mac:
+ brew install hugo
+ hugo version 验证安装成功
  
  执行这两行代码即可
  
2.参照文档搭建博客
+ 进入hugo官网 https://gohugo.io/ ，点击 Quick Start，则有搭建的全部步骤
  
  在搭建之前，先打开一个目录，例如进入到D盘，然后cmder(即：在此处打开命令窗口)
+ 直接从官网步骤的第二步开始抄代码，一直到第七步
  
  【2】create new site 

  `hugo new site xxx.github.io-generator`

  xxx要小写，是自己的github用户名，则会在当前目录创建这个网站
+ `code xxx.github.io-generator/`
  
  则会在VSCode里打开该目录
+ 【3】add a theme
  打开终端，继续照抄代码 
+ 【4】add some content 创建文章，自己命名即可
+ 可以找到该md文件，直接写博客了，**修改draft:true为draft:false**
+ 【5】Start the Hugo server
  可以看到网站地址了，ctrl+鼠标左键点进去就可以看到自己写的博客
+ 【6】Customize the Theme
  配置主题，在VSCode里ctrl+P搜config.toml文件在哪，
语言改成zh-Hans，即简体中文，title也可以改一下
+ 【7】Build static pages
  新开一个终端，**刚刚的不要关**，运行hugo。则创建一个新的目录public，这就是博客站点
+ hugo server -D 可以预览草稿 
  
  hugo server 预览非草稿

  至此，本地就可以看到自己用hugo搭建的博客了