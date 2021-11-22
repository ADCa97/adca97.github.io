---
title: WSGI
top: false
cover: false
toc: true
mathjax: true
date: 2021-11-10 11:42:54
password:
summary:
tags:
    - Web
categories:
---
## 为什么需要WSGI？
---
首先，我们明确一下Web应用处理请求的具体流程：
1. 浏览器发送一个HTTP请求
2. 请求转发至对应的Web服务器
3. Web服务器将请求转交给Web应用程序，Web应用程序处理请求
4. Web应用程序将请求结果返回给Web服务器，由Web服务器返回用户响应结果
5. 浏览器收到响应，向用户展示

其中，第3、4步Web服务器需要和Web应用程序进行通信，为了避免鸡同鸭讲的情况，规范它们之间的通信行为，WSGI应运而生。

## Web Server Gateway Interface
---
WSGI全称Python Web Server Gateway Interface，指定了Web服务器和Python Web应用程序或Web框架之间的标准接口，以提高Web应用程序在一系列Web服务器间的移植性。具体可参考[官方文档PEP 333](https://www.python.org/dev/peps/pep-0333/)。

具体的，WSGI应用程序接口是作为一个可调用对象实现的，比如一个函数、方法、类或者一个具有`__call__`方法的实例。该对象应该接受两个参数，返回一个可迭代对象：

1. **environ**: 带有环境变量的字典
2. **start_response**: 一个回调函数，用于向服务器发送HTTP状态和HTTP报头。该函数只能调用一次，其接收两个参数，一个是HTTP响应码，一个是一组`list`表示的HTTP Header，每个Header用一个包含两个`str`的`tuple`表示。

## 实战
---
接下来，我们编写`hello.py`，一个符合WSGI标准的HTTP处理函数：
```
# hello.py
def application(environ, start_response):
    status = "200 OK"
    response_headers = [("Content-Type", "text/html")]
    start_response(status, response_headers)
    path = environ["PATH_INFO"][1:] or "hello"
    return [b"<h1> Hello %s </h1>" % path.encode()]
```
然后，再编写一个`server.py`，负责启动WSGI服务器，加载`application()`函数：
```
# server.py
from wsgiref.simple_server import make_server
from hello import application


def main():
    server = make_server('localhost', 8001, application)
    print('Serving HTTP on port 8001...')
    server.serve_forever()


if __name__ == '__main__':
    main()
```
之后运行`python server.py`来启动WSGI服务器，打开浏览器，输入`http://localhost:8001/`就可以看到结果了。





## References
+ <https://zhuanlan.zhihu.com/p/95942024>
+ <https://rahmonov.me/posts/what-the-hell-is-wsgi-anyway-and-what-do-you-eat-it-with/>
+ <https://www.liaoxuefeng.com/wiki/1016959663602400/1017805733037760>
