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

**Write some code**
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

**Call code in an external package**

注意设置代理
```bash
go env -w GOPROXY=https://goproxy.cn,direct
```

```go
package main

import "fmt"

import "rsc.io/quote"

func main() {
	fmt.Println(quote.Go())
}
```

Add new module requirements and sums.
```bash
go mod tidy
```

## Create a Go module
<https://golang.google.cn/doc/tutorial/create-module>

***Start a module that others can use***
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

## Call your code from another module
1. Write code to call the Hello function, then print the function's return value.
    ```go
    package main

    import (
        "fmt"

        "example.com/greetings"
    )

    func main() {
        // Get a greeting message and print it.
        message := greetings.Hello("Gladys")
        fmt.Println(message)
    }
    ```
2. Edit the example.com/hello module to use your local example.com/greetings module.
    ```bash
    go mod edit -replace example.com/greetings=../greetings
    ```

## Return and handle an error
<https://go.dev/doc/tutorial/handle-errors>

## Return a random greeting
<https://go.dev/doc/tutorial/random-greeting>

## Return greetings for multiple people
<https://go.dev/doc/tutorial/greetings-multiple-people>

## Add a test
<https://go.dev/doc/tutorial/add-a-test>

## Compile and install the application
<https://go.dev/doc/tutorial/compile-install>
    