---
layout: post
title:  "使用JEKYLL搭建博客"
date:   2016-07-06 14:56:27
author: Ranger
overview: jekyll
categories: jekyll 搭建博客
---
学习前端已经有两个多月了，以前写后台的时候倒是没有想过去写一个blog，可能是因为自己的水平还不能产出一些好的文章吧。也或许是觉得写一个完整的站点真的会很麻烦。但是，随着时间的推移，越来越意识到，写博客真的是一件非常必要的事情，既可以纪录自己学习的知识，也可以锻炼自己的写作水平。于是，在这样的背景下我开始了博客搭建的道路。

一开始的想法是从零开始写一个blog(其实不明白为什么自己会有这样的想法，因为别人总跟我说你可以直接去CSDN或者博客园注册一个账号就可以写了啊，但我总觉得这不是我想要的)，然后就想到，那发博文是不是还要自己再写个富文本编辑器?完了是不是还要用node再写个评论模块?一想到这些，我就觉得我的思路可能错了，如果写个博客的成本这么高，而且还不能专注于内容，那别人是怎么做的呢?于是，怀着这样的疑问，我Google了如下关键字 **博客 快速 构建** ，然后发现了有两个工具我比较满意，一个是 `Wordpress`，另外一个就是我现在使用的**jekyll**，初步浏览了一些两个工具的文档之后，觉得jekyll的[文档](http://jekyll.bootcss.com/)看上去好简单，于是就使用了jekyll来搭建这个博客。

下面就是正式的上手工具了，首先是ruby的安装，windows环境下要安装[rubyinstaller](http://rubyinstaller.org/)，Linux下可以根据发行版的不同，选择不同的安装途径。