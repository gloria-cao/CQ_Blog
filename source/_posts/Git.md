---
title: Git
date: 2023-06-17 13:45:26
tags:

---

# Git

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
10. touch gitignore `创建隐藏文件，不提交到远程仓库`
11. git remote -v `查看当前仓库与远程仓库有哪些连接的 origin表示远程仓库的名字`

## 分支
1. git branch xxx `刚刚开始创建时，是**不会切换**到该分支里面的，按q退出`
2. git branch -b xxx `创建分支并切换到该分支里面`
2. git branch `查看分支`
3. git checkout  xxx`切换到分支`
4. 分支的文件是从主文件进行复制的，如果在分支里删除了文件，那么提交到主分支还是会存在，但是如果该文件在gitignore中那就不会回来了
5. git branch -d "分支名" `删除分支`；要是十分确认要删除那就将-d改为-D
6. git merge 分支名 `将别的分支合并到当前分支里面，如果有冲突，修改文本选择正确的即可`


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
