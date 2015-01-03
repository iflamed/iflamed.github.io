---
layout: post
title:  "PHP 的nginx 配置文件"
date:   2014-03-05 23:23:14
categories: 程序开发
tags: php nginx
---

## 配置文件如下
{% gist iflamed/52e07ef4704ce79320e7 %}


## 解释？
> 使用了nginx try_files来检测URL 是否可以访问，避免了使用if 的安全性问题。test.example.com.conf 的配置文件支持laravel 框架的子目录部署。由于try_files 和 alias 不能同时在一个location中使用，所以location /app 中使用if 来判断请求是否可以响应。

## 附带一个laravel 本身自带nginx 优雅链接的配置文件
{% highlight nginx %}
location / {
    try_files $uri $uri/ /index.php?$query_string;
}
{% endhighlight %}

Laravel [参考链接][laravel]

[laravel]: http://v4.golaravel.com/docs/4.2/installation#pretty-urls
