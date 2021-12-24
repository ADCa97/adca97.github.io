---
title: Git使用指南
top: false
cover: false
toc: true
mathjax: false
date: 2021-12-24 04:42:58
password:
summary:
tags:
    - Git
categories:
    - Others
img:
---

## 配置Git

```bash
git config [--global] user.name "user's name"
git config [--globla] user.email "user's email"
```

## 常用命令

+ `git status`
+ `git add <filename>`
+ `git commit -m "content"`
+ `git diff <filename>`
+ `git log [--pretty=oneline]`
+ `git reflog`查看命令历史

### 版本回退

在Git中，用`HEAD`表示当前版本，上一版本就是`HEAD^`，上上一版本就是`HEAD^^`，往上`n`个版本就是`HEAD~n`，使用`git reset`可以回退版本：
```bash
git reset --hard HEAD^

git reset --hard commit_id
```

### 撤销修改

```bash
# 丢弃工作区的修改
git restore <file>
# 把stage的修改撤销，重新放回工作区
git restore --staged <file>
```

### 删除文件

```bash
git rm <file>
```

## 远程仓库

### SSH配置

```bash
ssh-keygen -t rsa -C "youremail@example.com"
```

### 本地仓库与与远程空仓库关联

```bash
echo "# test" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:ADCa97/test.git
git push -u origin main
```

```bash
git remote add origin git@github.com:ADCa97/test.git
git branch -M main
git push -u origin main
```

删除远程仓库
```bash
# 查看远程仓库信息
git remote -v
# 删除
git remote rm origin
```

### 从远程仓库克隆

```bash
git clone git@github.com:<username>/<repositories>.git
# 本地创建分支关联到远程分支
git switch -c testbranch --track remotes/origin/testbranch
```

## 分支管理

### 创建与合并分支

创建并切换到`dev`分支
```bash
git switch -c dev
```

合并分支
```bash
# 切换到main分支
git switch main
# 将指定分支dev合并到当前分支main
git merge dev
```

删除分支
```
git branch -d dev
```

### 解决冲突

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。

使用`git log`查看分支的合并情况：
```bash
git log --graph --pretty=oneline --abbrev-commit
```

### 分支管理策略

[分支管理策略](https://www.liaoxuefeng.com/wiki/896043488029600/900005860592480)

