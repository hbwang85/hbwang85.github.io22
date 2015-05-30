---
layout: post
title: "开篇之作"
date: 2015-05-29 17:52:43 +0800
comments: true
categories: 
---
Today I will start my new blog journey. I decided to share my blogs to page. This is my first blog, I will just list the command that being useful for deploy blog.

1. rake new_post[“Blog Title”] 
2. rake generate
3. rake preview
4. rake deploy


保存你的代码

如前所述，rake deploy只是把生成的静态网页推送到了Github的Repo上去，但是你的博客的源码，就是这个octopress文件夹还需要地方保存，所以你可以新建一个Repo来保存源码：

1
2
3
4
git add .
git ci -s -m "Setup and config blogs for Github Pages"
git remote add myrepo *some public or private repo*
git push myrepo source


You can learn more detail from [Here](http://toughcoder.net/blog/2014/10/16/blogging-like-a-hacker-with-github-pages/)
http://octopress.org/docs/blogging/