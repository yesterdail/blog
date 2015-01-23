---
layout: post
title: "起源"
category : Lessons
---

## 1、一个最基本的框架

首先要知道什么是`github`及`Jekyll`?
    
简单说，github是一个具有版本管理功能的代码仓库。
	
Jekyll是一个静态站点生成器，它会根据网页源码生成静态文件。它提供了模板、变量、插件等功能。
	
整个思路到这里就很明显了。你先在本地编写符合Jekyll规范的网站源码，然后上传到github，由github生成并托管整个网站。

    .
    |-- _config.yml
    |-- _layouts
    |   |-- default.html
    |-- _posts
    |   |-- 2012-10-25-hello-wrold.md
    |-- index.html
		
[搭建一个免费的，无限流量的Blog----github Pages和Jekyll入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html)

## 2、Jekyll使用Liquid标记语言处理逻辑判断，输出模板变量

[Liquid](https://github.com/shopify/liquid/wiki/liquid-for-designers)有两种标记类型：输出和标签。

输出标记可以输出特定[模板变量](http://jekyllrb.com/docs/variables/)。

## 3、使用Markdown标记语言撰写博客

[Markdown](http://wowubuntu.com/markdown/index.html)的目标是实现「易读易写」，一份使用 Markdown 格式撰写的文件可以直接以纯文本发布。

## 4、实现不同的主题风格

[Bootstrap](http://jekyllbootstrap.com/)是Jekyll原作者推荐的学习案例，包括了博客的决大多数常见模块，如归档、分类、标签、评论、搜索、统计等。

更多的[Jekyll主题](http://jekyllthemes.org/)。

## 5、添加第三方评论系统

使用 Bootstrap 框架的 Jekyll 博客默认的评论系统是 Disqus，然而 Disqus 在国内访问速度和稳定性并不理想，而且无法和国内的各种社交网站耦合。目前最受欢迎、评价最高的应该是`多说`，本博客使用的评论系统就是多说。

[如何添加](http://liberize.me/tech/jekyll-use-duoshuo-comment-system.html)

## 6、遇到的一些问题

**Windows下运行 Jekyll Serve 命令没有错误，但无法启动？**

安装较低版本的Jekyll，运行如下命令

{% capture text %}Jekyll –v
Gem uninstall Jekyll
Gem install Jekyll –version “=2.1.1”
{% endcapture %}
{% include JB/liquid_raw %}








