### 设置代理

#### 1、什么是HTTP代理

HTTP代理的主要功能是为了将系统的HTTP流量转发到局域网内其他工具进行数据处理（比如Fiddler、Charles等工具均支持），此功能和系统WiFi连接下的手动指定HTTP代理服务器是相似的，不同的是Hodor在开启高阶模式以后可以转发系统代理无法捕获的HTTP流量，例如Flutter App的HTTP流量，如果您将流量转发到其他工具上进行处理，那么当前App的记录，重写功能将无效。    
  
此功能的精髓在于，你可以在电脑端查看和改写数据，毕竟电脑的屏幕更大，更方便查看，并且一些Hodor不支持的更高级的重写，也可以用其他工具实现。

#### 2、解密HTTPS注意事项
对于HTTPS协议如果你设置其他工具为代理服务器，比如Fiddler,你需要将Fiddler创建的用于解码HTTPS请求的根证书安装到当前设备上并信任这个证书，这样HTTP代理服务器才有能力解密HTTPS请。
    
网络上有很多关于使用Fiddler抓包iOS系统HTTPS请求的教程，安装证书这一块的操作方式是相同的，没有任何区别。
#### 3、怎么配置
这里拿Fiddler举例，首先你的代理服务器设备和本机需要在同一个局域网内，如果你在另外一台Mac上安装了Fiddler，那么你需要拿到这台Mac在局域网上的IP地址，并且拿到Fiddler监听的端口地址，那么仅需要在代理配置中添加该IP地址和端口号并选择该代理服务器作为目标服务器则可以生效了。
  
此功能的配置和使用Fiddler抓包iOS系统HTTP请求的配置方式也是类似的，只是一个在iOS系统的设置中配置，一个在此处配置。