# 重写规则
重写规则由2个部分组成，即`匹配规则`（对哪个请求执行重写）、`重写规则`（怎么重写）

### 《HTTP&WebSocket&TCP》请求重定向
重定向用于改变请求的目标地址和端口号，同时可以重新确定是否采用SSL/TLS加密，这种规则非常适用于测试工作中频繁切换测试服和正式服地址。
### 《HTTP&WebSocket》Path重写
HTTP Path 是指 HTTP URL 中主机名之后的部分，用于标识访问 Web 服务器上资源位置的路径。

    https://example.com/api/user?name=john&age=25
    
在这个例子中 `/api/user` 是Path，Path通常以`/`开头，我们在重写Path时，需要整个替换掉，填写的规则也必须以`/`开头，如果想将Path替换为空则仅填写`/`即可。

### 《HTTP&WebSocket》Query重写
HTTP Query 是一种通过 URL 传递数据的技术，它允许在 HTTP 请求的 URL 中通过 "?" 符号来传递参数和值。Query 由一个或多个键值对组成，并用 "&" 符号分隔。  

例如，以下 URL 包含一个带有两个参数（name 和 age）的查询字符串：

    https://example.com/api/user?name=john&age=25
    
在这个例子中 `name=john&age=25` 是Query字符串，是使用&拼接的多个键值对，在重写的时候，Hodor会将Query解析为类似字典的键值对（实际情况要更复杂些，因为要处理顺序和数组情况），然后对对应的Key、Value进行修改。  
另外这些参数名称和值都需要进行 URL 编码，例如 “value 1” 将会被编码为 “value%201”。 当然Hodor会为您自动处理这些转换，您不需要做额外的处理。

### 《HTTP&WebSocket》Header重写
HTTP Header一是一组键值对，您可以向HTTP的Header中添加或者删除某些值。但是这里有几个特殊处理其中Range、Content-Range、Content-Length、Content-Encoding、Content-Transfer-Encoding、Transfer-Encoding，这几个字段由系统控制，手动填写以后无效，Content-Type如果填写将覆盖系统设置的mime-type类型。

### 《HTTP》Body修改
HTTP Body可以传递非常多的编码方式。Hodor支持将数据解码成4种编码方式以键值对的方式做修改，text、json、x-www-form-urlencoded、multipart/form-data，当然你也可以动态替换掉整个Body部分，您仅需要预先将数据准备好，当匹配到对应请求以后会将Body进行替换。

#### 1、解码成text并用正则表达式进行修改

具体文档可以查看[示例文档](https://ximlu.github.io/hodor/regex_sample_zh.html)

#### 2、解码成JSON进行修改

具体文档可以查看[示例文档](https://ximlu.github.io/hodor/json_sample_zh.html)

#### 3、解码成x-www-form-urlencoded进行修改

具体文档可以查看[示例文档](https://ximlu.github.io/hodor/url_encoded_sample_zh.html)
  
#### 4、解码成multipart/form-data进行修改

具体文档可以查看[示例文档](https://ximlu.github.io/hodor/form_sample_zh.html)

### 《HTTP》Body替换

在App向Server发送请求前以及Server数据返回App以前，直接替换Body部分。

### 《HTTP》Code重写

Hodor可以更改HTTP状态码，也可以通过通过HTTP响应码重定向，选择301、302、307、308可以配置重定向地址。

### 《HTTP》Mock
主要用于某个特定的请求返回指定的内容，您可以理解为一个本地的HTTP服务器，对匹配上的请求返回设定好的内容。  

### 《TCP&WebSocket》数据修改
将TCP或WebSocket的上行和下行的数据流量转换为字符串或hex16后，使用正则表达式的方式对这些数据进行修改。具体文档可以查看[示例文档](https://ximlu.github.io/hodor/tcp_sample_zh.html)
  
***如果您有任何使用问题，可以通过email联系我们[hodorsoft@outlook.com](hodorsoft@outlook.com)，也可以在App Store给个五星好评，您的支持是我更新的最大动力。***
