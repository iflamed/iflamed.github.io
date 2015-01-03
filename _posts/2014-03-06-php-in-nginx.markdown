---
layout: post
title:  "PHP 的nginx 配置文件"
date:   2014-03-05 23:23:14
categories: 程序开发
tags: php nginx
---

## 简介
经典的LNMP 架构，在linux，nginx，mariadb，php 组合下搭建一个快速开发的web 环境。nginx 是一个高性能的服务器，通过异步，io复用的方式来提高服务器的性能。Mariadb 是mysql 被oricle收购之后的一个由开发者社区重新fork的一份新的开源数据库服务器。
在兼容mysql的同时，提供了比mysql更加高级、稳定的新功能。对于PHP 目前只推荐两个框架分别是laravel 和 yaf。laravel具有高度模块化，解耦合的特点，yaf 具有高性能的服务特点。
### php 在nginx 下面的cgi 配置文件：
{% gist parkr/931c1c8d465a04042403 php.conf %}

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
