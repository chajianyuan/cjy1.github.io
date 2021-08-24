---
title: git：github配置ssh_key
date: 2021-07-15 11:28:06
tags: git
category: 技术
---

如果我们想要`clone`或`pull`等自己github上的某个项目时，就需要先配置`ssh_key`，那么如何添加密钥呢❓

<!--more-->

#### 🦶步骤

##### 🌈 1. 生成密钥文件
```
cd ~/.ssh
ssh-keygen -t rsa -C "github上注册的邮箱"
> Enter file in which to save the key 指定生成文件位置
```
##### 🌈 2. 将`.pub`文件中的内容放在github中

![](https://github.com/chajianyuan/picture/blob/master/WX20210719-110018@2x.png?raw=true@w=200)

##### 🌈 3. 将本地的git仓库和SSH key关联上

```
ssh-add 你本地id_rsa地址
```

##### 🌈 4. 验证收否成功

```
ssh git@github.com
```

完成以上步骤就大功告成啦！🎉