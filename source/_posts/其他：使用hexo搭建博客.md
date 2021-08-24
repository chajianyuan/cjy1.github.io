---
title: 其他：使用hexo搭建博客
date: 2019-03-16 09:22:03
tags: 其他
category: 技术
---

<meta name="referrer" content="no-referrer"/>

### 一、:closed_book: 配置 github

1、首先注册、登录[github.com](https://github.com/)

2、在右上角选择[New repository](https://github.com/new)

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190316103736.png?raw=true)

在网页上输入 你的名字.github.io 显示正常，则新建成功

<!--more-->

### 二、:green_book:  环境安装（node、git）

1、安装[node.js](https://nodejs.org/en/)

2、安装 git[廖雪峰老师的安装教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/)

安装完成后，在开始菜单找到"Git"->"Git Bash"，名称都是 github 上面的

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190316104850.png)

3、安装 Hexo

`npm install -g hexo-cli`

[安装 cmder 流程](http://note.youdao.com/noteshare?id=1844b19b5f12367edd3460b6cf88d126)

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190316105545.png)

### 三、:blue_book: 设置

1、在合适的文件夹下新建文件夹 test,进入 test,右击选择 Cmder Here

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190316110343.png)

2、在窗口输入`hexo init blog`

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190316111949.png)

3、成功后提示`INFO Start blogging with Hexo!`

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190316111234.png)

4、访问 localhost:4000/，就可以访问初步的博客模样

![](https://github.com/chajianyuan/picture/blob/master/TIM%E5%9B%BE%E7%89%8720190316111314.png)

5、重新打开 cmd 输入

`ssh-keygen -t rsa -C "Github注册的邮箱地址"`

一路 enter 得到信息

`Your public key has been saved in /c/Users/user/.ssh/id_rsa.pub.`

找到该文件将里面的内容复制到[Github](https://github.com/settings/keys)

New SSH key ——Title：blog —— Key：输入刚才复制的—— Add SSH key

### 四、:orange_book: 配置博客

在 blog 目录下修改以下参数信息

网站的相关信息

```

title: #标题
subtitle: #副标题
description:  #站点描述，给搜索引擎看
author: #作者
language: zh-CN #语言
timezone:  Asia/Shanghai #
```

配置部署

```
deploy: #
  type: git #
  repo: # github地址
  branch: master
```

### 五、:notebook: 发表文章

在 cmd 中输入

```
hexo new "测试文章"
```

在给定的位置打开该文件，用 markdown 语法编辑

然后保存

`hexo clean` #清除缓存，网页正常情况下可以忽略此条命令

`hexo generate` #生成

`hexo server` #启动服务预览

最后发布到网上执行`hexo deploy` #部署发布

在网页上输入 你的名字.github.io 就可以看到已经发布的博客

### 六、:bug: bug fix

1、如果在执行 hexo deploy 后,出现 error deployer not found:github 的错误，执行：

`npm install hexo-deployer-git --save`

2、如果部署后出现 404，查看 github 数据源是否在 master 分支下
