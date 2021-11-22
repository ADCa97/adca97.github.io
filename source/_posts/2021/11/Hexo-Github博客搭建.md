---
title: Hexo+Github博客搭建
top: false
cover: false
toc: true
mathjax: false
date: 2021-11-22 17:49:09
password:
summary:
tags:
categories:
    - Web
img:
---

## Ubuntu安装Node.js
参见<https://github.com/nodesource/distributions/blob/master/README.md>，使用如下命令安装Node.js：
```bash
curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -
sudo apt-get install -y nodejs
```
安装完成后，输入`node -v`和`npm -v`，如果出现版本号，即代表安装成功。

同时，为npm添加国内镜像源：
```bash
npm config set registry https://registry.npm.taobao.org
```

## 新建Github仓库
仓库名必须设置为`${username}.github.io`，其中`${username}`为你的Github账户名。

之后点击`Settings->Pages`，`Source`选择`main`分支。

## 安装Hexo
```bash
npm install -g hexo-cli
```
安装完后输入`hexo -v`验证是否安装成功。

## 本地项目创建与配置
新建一个文件夹，如`myBlog`，进入该目录，输入`hexo init`初始化文件夹，接着输入`npm i hexo-deployer-git`安装npm相关依赖。

打开`_config.yml`，修改`deploy`项如下：
```
deploy:
  type: git
  repository: git@github.com:${username}/${username}.github.io.git
  branch: main
  message: 'hexo blog deploy'
```

## 写文章、发布文章
+ `hexo new post "article title"`，新建一篇文章
+ `hexo g`生成静态网页
+ `hexo s`可以本地预览效果
+ `hexo d`上传到github上


## 备份与同步
```bash
git remote add origin git@github.com:${username}/${username}.github.io.git
git push -u origin master
```


## References
+ <https://godweiyang.com/2018/04/13/hexo-blog/>
+ <https://github.com/blinkfox/hexo-theme-matery/blob/develop/README_CN.md>