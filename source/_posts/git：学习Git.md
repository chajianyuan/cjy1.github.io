---
title: git：学习Git
date: 2019-09-09 17:45:23
tags: git
category: 技术
---

<meta name="referrer" content="no-referrer"/>

<img src="https://github.com/chajianyuan/picture/blob/master/1631616508997_.pic.jpg?raw=true" width="600px" />

<!--more-->

### 一、Git 简介

Git 是目前世界上最先进的分布式版本控制系统。

### 二、集中式和分布式的区别

#### 1、集中式版本控制系统

提到集中式版本控制，大家首先想到的就是`SVN`，集中式版本控制系统中版本库是集中存放在中央服务器上的，而干活的时候，用的是自己的电脑，所以要先从中央服务器拿到最新的版本，然后开始干活，干完活再把自己的活推送到中央服务器，最大的缺点就是必须联网才能工作。

#### 2、分布式版本控制系统

每个人的电脑都是一个完整的版本库，这样，你工作的时候就不需要联网了，因为版本库就在自己的电脑上，多人协作时，只需要把各自的修改推送给对方就可以看到对方的修改了。

### 二、Git 指令

#### 1、`git clone git@server-name:path/reponame.git` 从远程克隆

#### 2、`git remote add origin git@server-name:path/reponame.git` 关联一个远程仓库

#### 3、`git init` 初始化一个仓库

初始化一个新的git仓库，或者重新初始化已存在的仓库

#### 4、创建与合并分支

在每次提交时，Git都将他们串成一条时间线，这条时间线只有一条叫做主分支（master），HEAD 指向当前分支

1）创建 dev 分支，并切换到 dev 分支

`git checkout -b dev` 或者`git switch -c dev`

等同于

```
git branch dev
git checkout dev 或者 git switch dev
```

2）查看当前分支`git branch`

3）将 dev 分支合并到 master`git merge dev`

> **PS: merge和rebase有什么区别❓**
> ```
> dev                 ✅ -- ✅ 
>                   /                
>                  /                
>                 /               
> matser  ⭕️ -- ⭕️ -- ⭕ --️️ ⭕
> ```
> * merge
>   * 特点：会自动创建一个新的commit
>   * 优点：真实记录commit
>   * 缺点：commit繁杂
> 
> ```
> dev                 ✅ -- ✅ -- ✅（多了一次合并的commit）
>                   /           /
>                  /           /
>                 /           /
> matser  ⭕️ -- ⭕️ -- ⭕ --️️ ⭕ 
> ```
> 
> * rebase
>   * 特点：合并之前的commit地址
>   * 优点：得到更简洁的commit历史
>   * 缺点：如果合并代码时出现了问题，不容易定位，因为重写了commit history
>```
> dev                ⭕ -- ⭕️️ -- ✅ -- ✅ 
>                  /                
>                 /                
>                /               
> matser  ⭕️ -- ⭕️
> ```

#### 5、添加文件到 Git 本地仓库

1）使用`git add <file>` ，注意，可以反复多次使用，添加多个文件（放到暂存区）；

2）使用`git commit -m <message>` 提交到本地仓库（放到工作区）。

**注意：** < message >存在规范，不能随便写，例如修改了哪个文件或者新增了哪个文件

`commit message格式`

```
<type>(scope): <subject>
```
**type(必须)：用于识别`git commit`的类别**

* feat: 新功能
* fix/to: 修复bug
  * fix: 适合于一次提交直接修复问题
  * to: 适合于多次提交。最终修复问题提交时使用fix
* docs: 文档
* style: 格式（不影响代码运行的变动）
* refactor: 重构（既不是新增功能，也不是修复bug）
* perf: 优化相关，比如提升性能、体验
* test: 增加测试
* chore: 构建过程或辅助工具的变动
* revert: 回滚到上一个版本
* merge: 代码合并
* sync: 同步主线或分支的bug

**scope(可选)：用于说明commit影响的范围**

**subject(必须)：`commit`目的的简短描述**

#### 6、`git push -u origin <name>` 推送到远程 master 分支

如果远程仓库没有对应的分支，则使用`git push --set-upstream origin <name>`创建远程分支

#### 7、`git pull -u origin <name>` 将最新的提交拉取下来

#### 8、`git status`查看工作区的状态

可以查看本地未提交的代码中，修改了哪些文件。

#### 9、`git diff <file>` 查看具体修改了什么内容

执行`git diff`可以查看所有具体修改，也可以指定查看具体的文件修改

#### 10、`git log --pretty=oneline` 查看历史记录

#### 11、版本回退

1) `git reset --hard commit_id`

**场景**：如果想撤销之前的某个版本，但是又想保留该目标版本之后的版本，记录下整个版本变动流程

`HEAD` 表示当前版本，上一个版本`HEAD^` ，上上个版本`HEAD^^` ，以此类推，往上 100 个版本是`HEAD~100`

**具体操作**：

```
1. git log 查看版本号
2. git reset --hard 目标版本
3. git push -f origin 分支名
```

<!--穿梭前，用`git log` 查看提交历史，以便确定要回退到哪个版本。-->

<!--重返未来，用`git reflog` 查看历史命令，以便确定要回到未来的哪个版本。-->

2） `git revert（反做）`

**场景**：如果想恢复到之前某个提交的版本，并且那个版本之后的提交都不要了

**具体操作**：
```
1. git log 查看版本号
2. git revert -n 版本号
3. git commit -m "版本名"
4. git push
```

#### 12、`git checkout -- file` 丢弃工作区的修改

1）文件自修改后还没有放到暂存区，现在撤销修改就回到和版本库一模一样的状态；

2）文件已经添加到暂存区后，又做了修改，现在撤销修改就回到添加到暂存区后的状态。

#### 13、删除文件

本地文件管理器删除文件`rm file` 后，使用`git status`可以 查询哪些文件被删除了：

1）如果确定要删除,使用`git rm file` ，并且`git commit`

2）如果误删，则恢复删除的文件`git checkout -- file`


#### 14、`git log --graph` 查看分支合并图

#### 15、bug 分支

例如，你正在 dev 分支上进行工作到一半，突然接到要修复一个代号 101 的 bug 任务

1）把当前工作现场储藏起来`git stash` ；

2）创建分支修复 bug，修复完之后 commit。切换到 master 分支完成合并，最后删除新创建的 bug 分支；

3）恢复未做完的 dev 工作现场

​ 使用`git stash list` 查看工作现场

​ （a）用`git stash apply` ，然后使用`git stash drop` 删除 stash 内容。使用`git stash apply stash@{0}` 恢复指定的 stash;

​ （b）使用`git stash pop` 恢复的同时能把 stash 内容也删除了。

在 master 分支上修复 bug，想要合并到当前的 dev 分支，可以使用`git cherry-pick <commit>` ,把 bug 提交的修改复制到当前分支，避免重复劳动。

#### 16、 删除分支

* 删除本地分支：`git branch -D <name>` 

* 删除远程分支： `git push origin -d <name>` 

* 删除包含fix的所有分支：`git branch | grep 'fix*' | xargs git branch -d`

* 删除当前分支以外的其他所有分支：`git branch | xargs git branch -d`

> :loudspeaker: 删除分支时需要切换到除被删除分支之外的分支

> 解释一下👇
> |: 管道命令，用于将一串命令串联起来。前面命令的输出可以作为后面命令的输入
> grep: 搜索过滤命令，使用正则表达式
> xargs: 参数传递命令，用于将标准输入作为命令的参数传给下一个命令

#### 17、查看远程仓库的信息用`git remote` 或`git remote -v`

#### 18、`git tag <name>` 打标签

为什么要打标签？四个字：**以示重要**，比如说使用tag标记发布节点（v1.0、v2.0等）

1）切换到需要打标签的分支上

```
git branch
git checkout <tagname>
```

2）打标签`git tag <tagname>`

3）查看所有标签`git tag`

4）查看指定标签信息`git show <tagname>`

5）删除标签 `git tag -d <tagname>`

6）推送一个本地标签`git push origin <tagname>`

7）推送全部未推送过的本地标签`git push origin --tags`

8）删除一个远程标签`git push origin :refs/tags/<tagname>`

#### 19、`git bisect` 查找哪一次代码提交引入了错误 

**原理**：二分法

举个栗子：一共有101次提交

**使用流程**：

 1） 检查代码提交记录 `git log --pretty=oneline`

 2） 启动查错 `git bisect start [终点commit] [起点commit]`
    
终点是最近一次的提交，起点是更久之前的提交

```
git bisect start [第101次commit] [第1次commit]
```

执行上述命令完之后，代码库会切换到上述范围正中间的那一次提交(也就是第51次提交)

 3）此时运行代码，如果代码运行正常，则使用`git bisect good`标记本次提交是没有问题的，此时代码会自动切换到后半段中点的版本（也就是第76次提交）

 4） 继续运行代码，如果代码运行不正常了，则使用`git bisect bad`标记本次提交是有问题的，此时代码会自动切换到本次提交到上一次提交的中点（也就是第63次提交）
 
 5） 不断重复上述第3、4步骤，就能找到出问题的那次提交
 ![](https://github.com/chajianyuan/picture/blob/master/1661616730056_.pic.jpg?raw=true)
 
 6） 退出查错，回到最近一次提交`git bisect reset`


> * 参照 [如何规范你的Git commit](https://mp.weixin.qq.com/s/vzgST0ko-HZVkFFiSZ2xGg)
> * 参照 [git bisect 命令教程](http://www.ruanyifeng.com/blog/2018/12/git-bisect.html)