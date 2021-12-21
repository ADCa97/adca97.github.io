---
title: LearnGo
top: false
cover: false
toc: true
mathjax: false
date: 2021-12-06 20:55:10
password:
summary:
tags: Go
categories: Go
img:
---

## 安装Go
<https://golang.google.cn/doc/install>

## Get started with Go
<https://golang.google.cn/doc/tutorial/getting-started>

## Create a Go module
<https://golang.google.cn/doc/tutorial/create-module>

### Start a module that others can use
1. 创建`greetings`目录

2. 运行`go mod init`命令
    ```bash
    go mod init example.com/greetings
    ``` 

3. 编辑`greetings.go`
    ```go
    package greetings

    import "fmt"

    // Hello returns a greeting for the named person.
    func Hello(name string) string {
        // Return a greeting that embeds the name in a message.
        message := fmt.Sprintf("Hi, %v. Welcome!", name)
        return message
    }
    ```
    