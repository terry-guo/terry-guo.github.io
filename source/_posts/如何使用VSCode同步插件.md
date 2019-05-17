---
title: 如何使用VSCode同步插件
date: 2019-05-17 14:36:49
tags:
---

> 使用插件将目前配置保存到GitHub上，以后只需要从GitHub上获取，就可以一次性安装插件配置信息。适合在电脑重装系统的时候快速恢复配置，也适合家里和公司电脑同步配置 



## 1.Setting Sync插件 

首先在VSCode里面搜索Setting Sync插件，安装好后重新加载激活

![](如何使用VSCode同步插件\01.png)



## 2.生成令牌GitHub Token 

打开编辑器，在打开任意文件，按下快捷键 `Shift + Alt + U`快捷键备份(上传) ,浏览器会跳转到全球最大的同性交友网站登陆，登录你的github账号，在下面页面中点击 Generate new token 生成令牌

![](如何使用VSCode同步插件\02.png)



点击上面按钮后会来到下面页面，填写备注，勾选gist，然后点击绿色的 Generate token按钮

![](如何使用VSCode同步插件\03.png)

这时候就得到了如下的token

![](如何使用VSCode同步插件\04.png)

## 3.执行备份

将上面生成的token输入到vscode的命令行中，`ctrl + P`可打开命令行，输入完命令之后回车，这时候会执行上传操作，成功之后会有如下提示。上传插件成功之后可以在控制台查看一些信息，如GitHub Token 和 GitHub Gist

![](如何使用VSCode同步插件\05.png)



## 4.保存token和id

将上述成功的 GitHub Token 和 GitHub Gist 保存在文本里面，可以上传到网盘什么的。

可以在控制台查看GitHub Token 和 GitHub Gist。也可以在settings.json中查看GitHub Gist ，在github中查看公告生成的GitHub Token 

![](如何使用VSCode同步插件\06.png)

![](如何使用VSCode同步插件\07.png)



## 5.恢复下载

按快捷键 ` shift+alt+d  ` 或 `ctrl+p `  输入 `>sync`点击Download Settings把 GITHUB GIST 的内容粘贴然后回车，即可下载

![](如何使用VSCode同步插件\08.png)

![](如何使用VSCode同步插件\09.png)

正常来说上面右下角会显示下载进度，如果不能下载成功很大概率是因为网络问题，打开小飞机之后再试试。



