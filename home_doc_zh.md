### Hodor使用手册

HTTP是一款基于IP协议的抓包工具，现阶段应用市场上绝大部分的抓包软件均是通过系统HTTP代理做的数据捕获，而Flutter开发的软件通过一些技术手段绕过了系统HTTP代理。但是Hodor是基于IP协议实现的，更底层，因此能抓到所有的数据流量。除了Flutter，很多原生App也会绕过系统HTTP代理，但是如果你使用Hodor所有的HTTP流量都可以抓到。

#### 1、过滤器使用手册

你可以设定一些过滤规则以便抓取指定的请求。  
具体文档可以查看[使用文档](https://ximlu.github.io/hodor/record_zh.html)

#### 2、重写使用手册

你可以设定一些列的规则以便调试客户端或服务器。  
具体文档可以查看[使用文档](https://ximlu.github.io/hodor/rewrite_zh.html)

#### 3、HTTP代理使用手册

你可以将系统流量转发到指定HTTP代理服务器，以便更好的处理数据。  
具体文档可以查看[使用文档](https://ximlu.github.io/hodor/proxy_zh.html)



