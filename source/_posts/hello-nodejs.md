---
title: node.js 学习
date: 2017-05-29
tags: Node.js
---

#### nvm 管理 node.js 版本

#### npm node.js包管理工具
<!-- more -->

npm是随同node.js一起安装的

设置npm国内淘宝代理镜像

    npm config set registry https://registry.npm.taobao.org 

#### 非阻塞式读取文件

    var fs = require("fs");

    fs.readFile("main.js", function(err, data){//回调
        if (err) {
            return console.error(err);
        }
        console.log(data.toString());
    });

    console.log("END");