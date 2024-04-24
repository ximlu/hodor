### Hodor使用手册

HTTP是一款基于IP协议的抓包工具，现阶段应用市场上绝大部分的抓包软件均是通过系统HTTP代理做的数据捕获，而Flutter开发的软件通过一些技术手段绕过了系统HTTP代理。由于Hodor是基于IP协议实现的，更底层，因此能抓到所有的数据流量。除了Flutter，很多常规抓包工具无法抓取流量的App通过Hodor也能捕获。

#### 1、过滤器使用手册

通过设定一些过滤规则以便抓取指定的请求。  
具体文档可以查看[使用文档](https://ximlu.github.io/hodor/record_zh.html)

#### 2、重写使用手册

通过预设规则以调试客户端或服务器的网络流量。  
具体文档可以查看[使用文档](https://ximlu.github.io/hodor/rewrite_zh.html)

#### 3、脚本使用手册

Hodor通过使用JavaScript来扩展一些特别的功能。  
具体文档可以查看[使用文档](https://ximlu.github.io/hodor/script_zh.html)

#### 4、HTTP代理使用手册

你可以将系统流量转发到指定HTTP代理服务器，以便控制数据处理。  
具体文档可以查看[使用文档](https://ximlu.github.io/hodor/proxy_zh.html)

#### 5、局域网功能说明
Hodor在局域网下可以捕获其他设备的流量（例如Android），但是是无法捕获这些设备的所有流量的，因为Hodor在底层做了很多工作才能捕获到，但是安装了Hodor的苹果设备可以通过Hodor的HTTP代理功能将捕获到的流量转发到局域网其他设备。

***如果您有任何使用问题，可以通过email联系我们[hodorsoft@outlook.com](hodorsoft@outlook.com)，也可以在App Store给个五星好评，您的支持是我更新的最大动力。***



