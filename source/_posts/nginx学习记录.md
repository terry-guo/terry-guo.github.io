---
title: nginx学习记录
date: 2019-02-18 12:02:55
tags:
---

## 前端配置nginx实现跨域

> 前言：以前做过jsonp实现跨域，不过这种需要服务端配合。现在的前端项目，比如vue，react等，在配置项目的脚手架中就带有跨域设置，也可以自己写一个node服务来跨域，今天来简单学习一下用nginx来实现跨域。

 

### 1.什么是nginx

nginx是一个高性能的HTTP和反向代理[服务器](https://www.baidu.com/s?wd=%E6%9C%8D%E5%8A%A1%E5%99%A8&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)，也是一个IMAP/POP3/SMTP代理服务器。 nginx的作用是:反向代理，负载均衡。其特点是占有内存少，并发能力强。 



### 2.nginx安装

#### 2-1 windows版：

> nginx下载地址：http://nginx.org/en/download.html 

nginx官网提供了三个类型的版本：

- Mainline version：Mainline 是 Nginx 目前主力在做的版本，可以说是开发版 .
- Stable version：最新稳定版，生产环境上建议使用的版本 
- Legacy versions：遗留的老版本的稳定版 

​      建议使用稳定版。下载之后解压，解压路径中尽量不要有中文，实际上各种环境配置，软件安装等目录尽量都不要用中文，因为中英文字符编码不一样。

解压之后的目录就是这样

![nginx_01](nginx学习记录/nginx_01.png)

windows中常用的操做命令，一下命令全在上面根目录进行，用系统自带命令行，比如cmd。

1.启动nginx。实际上点击nginx.exe也能打开nginx，但是不容易关闭，需要到任务管理器中找到相关服务强行停止掉，建议使用下面命令行开启服务

~~~
start nginx
~~~





```
location  = / {
  # 精确匹配 / ，主机名后面不能带任何字符串
  [ configuration A ] 
}

location  / {
  # 因为所有的地址都以 / 开头，所以这条规则将匹配到所有请求
  # 但是正则和最长字符串会优先匹配
  [ configuration B ] 
}

location /documents/ {
  # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
  # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
  [ configuration C ] 
}

location ~ /documents/Abc {
  # 匹配任何以 /documents/ 开头的地址，匹配符合以后，还要继续往下搜索
  # 只有后面的正则表达式没有匹配到时，这一条才会采用这一条
  [ configuration CC ] 
}

location ^~ /images/ {
  # 匹配任何以 /images/ 开头的地址，匹配符合以后，停止往下搜索正则，采用这一条。
  [ configuration D ] 
}

location ~* \.(gif|jpg|jpeg)$ {
  # 匹配所有以 gif,jpg或jpeg 结尾的请求
  # 然而，所有请求 /images/ 下的图片会被 config D 处理，因为 ^~ 到达不了这一条正则
  [ configuration E ] 
}

location /images/ {
  # 字符匹配到 /images/，继续往下，会发现 ^~ 存在
  [ configuration F ] 
}

location /images/abc {
  # 最长字符匹配到 /images/abc，继续往下，会发现 ^~ 存在
  # F与G的放置顺序是没有关系的
  [ configuration G ] 
}

location ~ /images/abc/ {
  # 只有去掉 config D 才有效：先最长匹配 config G 开头的地址，继续往下搜索，匹配到这一条正则，采用
    [ configuration H ] 
}

location ~* /js/.*/\.js
```





```
server {
        listen       80;
        server_name  www.a.com;
        access_log  logs/test.access.log;
        # 匹配以/apis/开头的请求
        location ^~ /apis/ {
            proxy_pass http://www.b.com/;  #注意域名后有一个/
        }
        location / {
            root html/a;
            index index.html index.htm;
        }
        #
        error_page   500 502 503 504  /50x.html;
        location = /50x.html {
            root   html;
        }
    }
```



- 加/的情况，访问`www.a.com/apis/login.json`会得到`www.b.com/login.json`（符合预期的）,使用b文件夹作为/目录来访问
- 不加/的情况,访问`www.a.com/apis/login.json`会得到`www.b.com/apis/login.json`（不符合预期）,使用b文件下的apis作为根目录进行访问