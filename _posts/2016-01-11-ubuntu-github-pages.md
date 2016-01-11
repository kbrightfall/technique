---
layout: post
title: "Ubuntu利用github-pages搭建博客"
date: 2015-01-11 14:07:11
tags: 教程
categories: [Linux]
description: 怎样在github上搭建自己的博客网站
---

## 介绍
对于诸如在校学生等群体来说，出于分享知识的需要，一个好用的而且免费的博客是很有必要的，这里我们介绍一下怎么利用开源网站github提供的空间搭建免费的博客，主要是利用github-pages及jekyll模板引擎来搭建静态博客网站，本教程是在ubuntu14.04的系统下进行讲解，下面介绍具体搭建流程：

## 第一步：在github上申请帐号
首先我们需要在[github](https://github.com/)上申请自己的帐号,这里帐号名称用your_account代替，在这里，我们可以利用帐号主页来建立我们的博客，也可以利用项目的主页来建立我们的博客，这里我们演示如何通过项目主页来建立博客：新建一个repository,名称用your_repository代替,这样我们的项目主页是*http://your_account.github.io/your_repository*，后续我们的博客地址就是这个，我们可以利用自己购买的域名绑定空间，这里不作描述。


## 第二步：搭建本地环境
这里我们使用jekyll模板引擎来搭建博客，jekyll是用ruby写的，所以我们首先在安装ruby环境,在ubuntu14.04上，由于系统仓库中的ruby版本太旧，新的jekyll需要ruby2.0以上版本，所以这里我们直接在[ruby的官方网站](http://www.ruby-lang.org/en/downloads/)上下载源码进行编译，步骤如下：

- 下载ruby-2.3.0.tar.gz,并解压到ruby-2.3.0目录中
{% highlight bash %}
tar xvf ruby-2.3.0.tar.gz
{% endhighlight bash %}

- 编译与安装ruby2.3
 {% highlight bash %}
 cd ruby-2.3.0
 ./configure
 make
 sudo make install
 {% endhighlight bash %}

- ruby会被安装到/usr/local/bin中,我们需要从gem源中安装jekyll
{% highlight bash %}
cd /usr/local/bin
sudo ./gem install jekyll
{% endhighlight bash %}

- 安装成功后，我们需要从jekyll新建模板，我们也可以从[jekyll模板网站](http://jekyllthemes.org/)下载主题使用，里面有很多不错的模板可供使用。
{% highlight bash %}
jekyll new your_site_name
{% endhighlight bash %}

- 本地测试网站
{% highlight bash %}
cd your_site_name
jekyll serve --safe --watch
{% endhighlight bash %}

- 随后我们便可以从浏览器中访问本地的网站，网址是**http://127.0.0.1:4000/your_site_name/**

## 第三步：将网站同步到Github项目主页
这部分主要是关于Git的使用，关于Git的使用请参考网上的其它教程，这里不展开说，我们首先进入jekyll新建的网站的目录下，利用如下步骤将本地网站同步到github-pages上面
{% highlight bash %}
git init
git checkout --orphan gh-pages
git add *
git commit -m "######"
git remote add origin https://github.com/your_account/your_repository.git
git push origin gh-pages
{% endhighlight bash %}
提交成功后，等待几分钟我们便可以通过项目网站**http://your_account.github.io/your_repository**访问我们的博客了

## 第四步：写博客并更新同步到github-pages
建立好基本的博客系统之后，我们写博客只要在本地的_posts目录中新建页面，很方便的是我们可以直接利用markdown书写我们的博客，jekyll会自动将其转化为网页形式，所以我们在这里建立格式为Year-month-day-title.md的markdown文件,如2016-01-11-welcome-to-jekyll.md，随后在写完之后利用git命令同步到github-pages中，便可以看到更新后的网站了。
