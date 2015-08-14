---
layout: post
title: "nodejs study points"
date: 2015-08-14 11:33:12 +0800
comments: true
categories: 
---

1. Install express  
express is a framework for nodejs. Its latest version is after 4.0. Original after we install the express, the terminal tool is installed together. For the the version after 4.0 they should be installed separately. You can install the express framework by :
```
npm install -g express
```
However, this command is just for installing the framework, if you want to install teh terminal command tool, you should install the generator as below:   
```
npm install -g express-generator  
```
Reminder that you should execute al these commands as administrator, add "sudo"

2. express -t is deprecated, use express -e/--ejs instead.
