---
title: Hexo Hello World
date: 2017-04-25
tags: 
- hexo
- github
- Node.js
---

这是一个使用[Hexo](https://hexo.io/zh-cn/)和[github](https://github.com)搭建的个人博客网站，下面是我搭建这个博客的过程(windows系统下)

<!-- more -->

## 开始吧

### 安装工具
- 安装[git](https://git-scm.com/)
- 安装[Node.js](https://nodejs.org/en/)

然后在Git Bash Here里通过命令安装Hexo

    $ npm install -g hexo-cli

### 搭建网站

下面都是在Git Bash Here里执行命令

1.创建网站的根目录

    $ hexo init D:/blog

2.进入目录

    $ cd D:/blog

3.初始化网站，[Hexo](https://hexo.io/zh-cn/) 将会在指定文件夹中新建所需要的文件，这个过程可能有点慢

    $ npm install

### 启动[Hexo](https://hexo.io/zh-cn/) 服务

接着刚才的命令，在D:/blog目录下执行

    $ hexo server  或者  $ hexo s

现在就可以打开浏览器在地址栏中输入： localhost:4000

网站就这样出来了，是不是很神奇

### 创建仓库

刚才创建出来的网站只能在本地访问，想要能在网络上来访问就需要在[github](https://github.com)上创建一个仓库，名字格式为：zhanghangnice.github.io

创建出来是空的，我们还需要一些配置才行

### 修改配置

网站虽然是出来了，但是好像还木有一点自己的内容，那就接着改吧

在刚才创建的D:/blog目录下有个文件 _config.yml 修改里面的几个属性就可以看起来像是你自己的网站了

我自己的配置：

    title: 张杭的个人博客
    subtitle: 一个偏执的热血青年在偏执的道路上越陷越深
    description: 张杭 Android 
    keywords: 张杭 Android
    author: 张杭
    email: zhanghangnice@gmail.com
    language: zh-CN

	···

	deploy:
  		type: git
  		repo: https://github.com/ZhanghangNice/zhanghangnice.github.io.git
  		branch: master


更多配置属性介绍可以参考[这里](https://hexo.io/zh-cn/docs/configuration.html)


### 见证奇迹

前面所有的都配置好后，执行下面的命令重新生成网站，生成的整个网站在public文件下

    $ hexo generate  或者  $ hexo g

执行下面的命令将生成好的网站提交到[github](https://github.com)

    $ hexo deploy  或者  $ hexo d

上面的命令执行完后，就可以在浏览器地址栏输入[zhanghangnice.github.io](zhanghangnice.github.io)

这样你就能在有网络的地方访问到你的网站了

很有趣吧···

### 其他

新建一篇文章

    $ hexo new <title>

查看[Hexo](https://hexo.io/zh-cn/) 版本信息

    $ hexo version

列出网站资料

    $ hexo list <type>

清除缓存文件 (db.json) 和已生成的静态文件 (public)

    $ hexo clean


最后是我遇到的问题

问题：修改配置文件 _config.yml 里面的属性后乱码

解决：将配置文件的编码格式改为UTF-8

