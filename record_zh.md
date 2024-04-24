### 抓包相关知识

#### 1、为什么Hodor可以抓取Flutter的流量而其他抓包软件做不到
因为应用市场上的抓包软件均是通过系统HTTP代理做的转发，而Flutter等一些软件通过一些技术手段绕过了系统HTTP代理。但是Hodor是基于IP协议实现的，更底层，因此能抓到所有的数据流量。除了Flutter，很多原生App也会绕过系统HTTP代理，但是如果你使用Hodor所有的HTTP流量都可以抓到。

#### 2、什么是CONNECT协议，为什么我的记录中有很多CONNECT请求

CONNECT协议是一种用于在客户端和服务器之间建立隧道连接的协议，通常用于SSL/TLS加密通信以及代理服务器。通过该协议，客户端可以直接与目标服务器通信，无法解密的HTTPS流量都会呈现为CONNECT。

#### 3、为什么我开启了MITM，部分请求还是显示的CONNECT
因为MITM解密仅支持通用的SSL/TLS，如果客户端对证书做了强校验，那么就无法解密，无法解密的请求均以CONNECT请求的方式记录。

#### 4、要合理使用Hodor抓包，必须要理解URL的组成部分
URL（Uniform Resource Locator），统一资源定位符，是用于标识互联网上资源位置的地址。它由若干个部分组成：

`scheme `：指定访问该资源所使用的协议，例如HTTP、HTTPS、FTP等。  
`host `：指定服务器的域名或IP地址。   
`port `：指定服务器提供该服务的端口号，如果没有明确指定则使用默认端口号。   
`path `：指定服务器上资源的具体路径，以斜线/开头。  
`query `：在URL中传递附加的信息参数，以问号?开头，多个参数之间用&连接，是一串键值对组合。  

例如

	http://example.com:8080/path/to/resource?foo=bar&foo1=bar1
scheme为`HTTP`  
host为`example.com`  
port为`8080`  
path为`/path/to/resource`  
query参数为`foo=bar&foo1=bar1`  
在匹配的时候使用这些组成部分单独做的匹配  

  
***如果您有任何使用问题，可以通过email联系我们[hodorsoft@outlook.com](hodorsoft@outlook.com)，也可以在App Store给个五星好评，您的支持是我更新的最大动力。***
