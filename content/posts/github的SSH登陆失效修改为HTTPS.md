---
title: "github的SSH登陆失效修改为HTTPS"
date: 2021-01-26T16:15:39+08:00
draft: false
---

向github push代码的时候，发现push报错

**kex_exchange_identification: read: Connection reset by peer**

尝试重新生成公钥密钥，然后更新github上的SSH Keys，发现不行

上网查找之后尝试了好几种方法，有修改.ssh/config文件的，但是没有生效，也有可能是网络问题，所以决定暂时将SSH方式修改成HTTPS方式，先将代码提交上去

实验过程中由于开了好几个终端，后来问题变成了这样：

git push的时候显示：
kex_exchange_identification: Connection closed by remote host
fatal: Could not read from remote repository.

参考这篇博客http://www.lao8.org/article_1319/ssh
发现产生原因是SSH连接数过多

修改方法是改大/etc/ssh/sshd_config文件的MaxSessions或者每次正常退出SSH

修改SSH->HTTPS方式步骤如下：

1. git remote -v

   查看使用的是哪种方式

   之前使用的是SSH，因此显示结果是

   origin  git@github.com:XXX/XXX.github.io.git (fetch)
   origin  git@github.com:XXX/XXX.github.io.git (push)

   XXX是人名，此处已略去

2. 通过以下这个命令设置SSH为HTTPS

   git remote set-url origin https://github.com/XXX/XXX.github.io.git

3. 首次push可以设置  git push -u origin master  我直接就git push了

4. push成功了，如图所示

![](../img/SSH2HTTPS.png)

