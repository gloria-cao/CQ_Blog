---
title: Git
date: 2023-06-17 13:45:26
tags:

---

# Git
Git官方文档：https://git-scm.com/docs

## 分布式版本控制
1. 没有中央服务器，每个人的电脑就是一个完整的版本库，工作的时候不需要联网，因为版本都在自己的电脑上。
2. 协同的方法：就是能看到对方更改了那些代码和文件 
## 集中式版本控制 SVN
1. 版本库是集中放在中央服务器的，在工作的时候，用的都是自己的电脑，所以首先 要从中央服务器得到 **最新的版本**，然后工作，工作完成后，需要把自己做完的工作推送到中央服务器。
2. **集中式版本控制系统是必须联网才能工作的，对网络要求比较高**

## 基本流程
1. 代码未提交时，代码此时在**工作区**  ，未追踪状态状态为Untracked | Unstage
2. git add .  `代码提交到暂存区`  已追踪状态 Stage
3. git commit -m "info"  `提交到本地仓库`
4. git commit -a -m "info" `合并add和commit两个命令`
4. git push  `推送到远程仓库`
5. git fetch `将远程仓库的代码放到本地仓库` + git diff`对比远程仓库和本地代码的区别，再进行合并`
5. git pull `将远程代码更新下来，但是会将工作区代码给更新掉`
6. git clone
7. git init `初始化git文件，默认处于主分支master，生成.git隐藏文件夹，git的所有操作都记录在该文件夹中`
8. git status `当前git状态`
9. git log `查看之前的版本`
10. touch .gitignore `创建隐藏文件，不提交到远程仓库`
11. git remote -v `查看当前仓库与远程仓库有哪些连接的 origin表示远程仓库的名字`

## 分支 | main
1. **主分支(主干 | 主线 | main | master)**

    包含所有最终修改的历史，反映项目的最终版本

    建议不要乱动主干。如果你编辑了一个小组项目的主干分支，你的改动会影响到其他人，而且很快会出现 **合并冲突**

2. **开发分支(集成分支 | develop | dev)**
  与主分支平行。该分支包含了为下一个版本所作的最新开发修改。它拥有该版本的最终源代码。
  当开发分支达到稳定状态并准备发布时，应与主干分支合并，并标记为发布版本。

  ![分支概述](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230618100812161.png)

  ![分支操作](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230618101425541.png)

3. git branch xxx `刚刚开始创建时，是**不会切换**到该分支里面的，按q退出`

4. git branch -b xxx `创建分支并切换到该分支里面`

5. git branch `查看分支`

6. git checkout  xxx`切换到分支`

7. 分支的文件是从主文件进行复制的，如果在分支里删除了文件，那么提交到主分支还是会存在，但是如果该文件在gitignore中那就不会回来了

8. git branch -d "分支名" `删除分支`；要是十分确认要删除那就将-d改为-D

9. git merge 分支名 `将别的分支合并到当前分支里面，如果有冲突，修改文本选择正确的即可`

10. 当我在本地创建了分支，但是远程仓库没有创建该分支时是无法将该分支推送到远程仓库中的 

   `git push --set-upstream origin a`

   通过这条命令推送到远程仓库

11. 

## gitignore
1. 配置忽略规则，并非所有文件都需要保存到版本库中，譬如日志文件、临时文件及工具生成的文件。
2. **touch .gitignore**
3. **检查.gitignore文件是否生效**  `git check-ignore -v{文件或者目录路径} 有输出即忽略掉了(如下图)，没输出即没有忽略`

    ![检查文件是否忽略](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230617214535822.png)
4. 简单配置
    每项配置独占一行。
     每行的内容可以是：文件/目录 的名称、路径 或 它们的模式匹配。 
### 模式匹配
1. 空行不匹配任何文件，因此常用作分隔符（以方便阅读）。  
2. `#`用于注释，\ 表示转义（如对 a!bc.txt，需改为 a\!bc.txt）。
3. * 可以匹配任何字符(0或多次)，? 可以匹配任何字符(1次)。（注意：它们都不可以匹配 / ）。
4. / 用于分隔目录：
   * / 在开头时，表示从项目根目录开始匹配。否则，下级都将匹配。
     	 举例：  /abc 只能匹配 /abc，不能匹配 /x/abc 或 /x/y/abc等
   * 当 / 在末尾时，只匹配目录，否则，则同名的目录和文件都将匹配。
     	举例：  /abc/ 只能匹配 /abc目录，不能匹配/abc文件。
     	举例：  abc/ 能匹配 /abc/ 或 /x/abc/ 或 /x/y/abc/等，不能匹配 /abc 或 /x/abc 等。

5. 原先被排除的文件，使用 ! 模式后该文件将会重新被包含。但如果了该文件的父级目录被排除了，那么使用 ! 也不会再次被包含。
6. [] 通常用于匹配一个字符列表，如：a[mn]z 可匹配 amz 和 anz。

7. ** 用于匹配多级目录，如 a/**/b 可匹配 "a/b", "a/x/b", "a/x/y/b" 等 。

## git 命令

```shel
usage: git [-v | --version] [-h | --help] [-C <path>] [-c <name>=<value>]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | -P | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           [--super-prefix=<path>] [--config-env=<name>=<envvar>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone     Clone a repository into a new directory
   init      Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add       Add file contents to the index
   mv        Move or rename a file, a directory, or a symlink
   restore   Restore working tree files
   rm        Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect    Use binary search to find the commit that introduced a bug
   diff      Show changes between commits, commit and working tree, etc
   grep      Print lines matching a pattern
   log       Show commit logs
   show      Show various types of objects
   status    Show the working tree status

grow, mark and tweak your common history
   branch    List, create, or delete branches
   commit    Record changes to the repository
   merge     Join two or more development histories together
   rebase    Reapply commits on top of another base tip
   reset     Reset current HEAD to the specified state
   switch    Switch branches
   tag       Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch     Download objects and refs from another repository
   pull      Fetch from and integrate with another repository or a local branch
   push      Update remote refs along with associated objects

```




## Git代码没写完想切换分支怎么办？

1. git  stash `可以保存当前的分支，然后在切换到别的分支`
2. git stash pop `当另一个分支的内容完成后，切换回来，使用该命令进行恢复即可`

## Git提交错分支了怎么办？

1. 当使用 git cz这种规范工具提交代码时

   git reset --soft HEAD^ `代码将回到暂存区`

2. vscode提交框进行提交，撤销也很方便

## Git在真实项目中分支流程

1. 当分配任务需要做a功能 时可以新创建一个分支

   git checkout -b A

2. 提交代码

   git add . `此时分支还在本地`

   git push --set-upstream origin A `将分支推送到远程仓库`
   
## 已提交的文件如何忽略
1. **.gitignore只能忽略那些没有被追踪过的文件**，所以先纳入版本管理后写入.gitignore是无效的
2. 解决方法：
     思路：先删除本地缓存再加入
       git rm -r --cached .
       git add .
       git status
3. **已被.gitignore忽略的文件是无法加入版本库的**
4. 解决方法
     思路：要纳入版本管理，先移除规则



## 以别的角色身份进行提交

1. git config --local user.name "xxx"
2. git config --local user.email "xxx.com"
3. ![以其他用户身份进行提交](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230618093820017.png)



## 文件误删

1. 文件已add过一次 ，git checkout a.txt

   ![git恢复文件流程图](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230618100006413.png)

# github



# 问题

1. 为什么每次push都不需要账号密码

   ![存放用户凭据](https://blog-images-1310572444.cos.ap-guangzhou.myqcloud.com/image-20230618091417320.png)
