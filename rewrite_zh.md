### 重写规则
重写规则由2个部分组成，即`匹配规则`（对哪个请求执行重写）、`重写规则`（怎么重写）

### Host重写
Host重写用于改变请求的目标地址和端口号，同时可以重新确定是否采用SSL/TLS加密，这种规则非常适用于测试工作中频繁切换测试服和正式服地址。
### Path重写
HTTP Path 是指 HTTP URL 中主机名之后的部分，用于标识访问 Web 服务器上资源位置的路径。

    https://example.com/api/user?name=john&age=25
    
在这个例子中 `/api/user` 是Path，Path通常以`/`开头，我们在重写Path时，需要整个替换掉，填写的规则也必须以`/`开头，如果想将Path替换为空则仅填写`/`即可。

### Query重写
HTTP Query 是一种通过 URL 传递数据的技术，它允许在 HTTP 请求的 URL 中通过 "?" 符号来传递参数和值。Query 由一个或多个键值对组成，并用 "&" 符号分隔。  

例如，以下 URL 包含一个带有两个参数（name 和 age）的查询字符串：

    https://example.com/api/user?name=john&age=25
    
在这个例子中 `name=john&age=25` 是Query字符串，是使用&拼接的多个键值对，在重写的时候，Hodor会将Query解析为类似字典的键值对（实际情况要更复杂些，因为要处理顺序和数组情况），然后对对应的Key、Value进行修改。  
另外这些参数名称和值都需要进行 URL 编码，例如 “value 1” 将会被编码为 “value%201”。 当然Hodor会为您自动处理这些转换，您不需要做额外的处理。

### Header重写
HTTP Header一是一组键值对，您可以向HTTP的Header中添加或者删除某些值。但是这里有几个特殊处理其中Range、Content-Range、Content-Length、Content-Encoding、Content-Transfer-Encoding、Transfer-Encoding，这几个字段由系统控制，手动填写以后无效，Content-Type如果填写将覆盖系统设置的mime-type类型。

### Body重写
HTTP Body可以传递非常多的编码方式。Hodor支持3种编码方式以键值对的方式做修改，json、x-www-form-urlencoded、multipart/form-data，当然你也可以动态整个替换掉body部分，您仅需要预先将数据准备好，当匹配到对应请求以后会将Body进行替换。
#### 解码成JSON进行修改
JSON重写采用匹配KeyPath, 替换或新增Value，或删除对应的Key以及Value的方式工作的。
##### 1、什么是KeyPath？ 
JSON的修改可以通过KeyPath的方式来替换或者删除某个值。  
KeyPath表示JSON的访问路径字符串，使用关键词`.`和`*`以及`[]`来设计的路径字符串，`.`用于字典取值，`*`和`[]`用于数组取值

	{
     "A": "a1", 
     "B": {
        "B1": "bbbb", // String类型
        "B2": 110  // Int类型
     }, 
     "C": [{
            "C1": "cccc"
        }, 
        {
            "C1": "ccccc"
        }]
	}
比如您想访问B2这个值，您的KeyPath应该是这样的  
`B.B2`  
如果您想访问第一个C1的值，您的KeyPath应该是这样的  
`C[0].C1` // 其中0是数组下标  
如果您想要定位到所有C1，您的KeyPath应该是这样的  
`C[*].C1` // 其中*表示通配符，匹配数组里所有的内容  
  
##### 2、json编码的数据是有类型，在修改数据的时候应当指定对应值的数据类型。  
*auto类型*   
如果您的值类型设定的auto,那么该值会被转换为和原值一样的数据类型，如果类型转换失败，那么则会抛出一个异常并存储在重写日志中，如果没有原值，那么将转换为String类型并插入到对应位置  
比如您想替换B2的值，KeyPath应当设置为`B.B2`，值您设置为`900`，且数据类型为`auto`, 那么这个数据会自动转换为Int类型。  

*指定值的数据类型*  
如果您指定了修改值的数据类型，那么在新增或替换的时候您设置值将转换为您指定的数据类型后再去新增或替换对应的值，同样的如果类型转换失败，那么则会抛出一个异常存储在重写日志中。  

#### 解码成x-www-form-urlencoded重写
x-www-form-urlencoded重写是解码成键值对，采用匹配Key, 替换或新增Value，或删除对应的Key以及Value的方式工作的。

具体来说，在 x-www-form-urlencoded 中，请求的每个参数都用“键=值”的形式表示，不同参数用 & 符号分隔开。例如：

	name=value1&age=value2&address=value3

这些参数名称和值都需要进行 URL 编码，例如 “value 1” 将会被编码为 “value%201”，在重写的时候您不需要手动进行URL编码处理，系统会自动为您处理。  

#### 解码成multipart/form-data重写

HTTP multipart/form-data是一种使用多个部分（multipart）构成的数据格式，常用于客户端向服务端发送带有文件上传的请求。

在multipart/form-data数据格式中，每一个表单项目由一个独立的部分（part）组成，每个部分之间由分隔符分隔。每个部分都可以包含一个头部信息（headers）以及与之相关联的内容（body），如文本、二进制数据等。headers中通常包含Content-Disposition、Content-Type等关键字描述了该部分的类型、名称以及编码方式等信息，而body则是实际携带的数据。

下面是multipart/form-data数据格式的示例

	POST /submit-form HTTP/1.1
	Host: example.com
	Content-Type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW
	Content-Length: 248
	
	------WebKitFormBoundary7MA4YWxkTrZu0gW
	Content-Disposition: form-data; name="text"
	
	Hello World!
	------WebKitFormBoundary7MA4YWxkTrZu0gW
	Content-Disposition: form-data; name="image"; filename="example.png"
	Content-Type: image/png
	
	(binary data)
	------WebKitFormBoundary7MA4YWxkTrZu0gW--
	
	
上面的示例展示了一个包含text和image两个表单项的multipart/form-data请求。其中，text表单项为普通文本，而image表单项则包含了一个名为example.png的文件。文本和文件数据分别位于不同的部分中，并且每个部分都有自己的content-type、名称以及body内容。

在重写规则中name、filename就是对应的Content-Disposition的name, filename，Hodor仅支持name和对应内容的改写。

### Code重写

Hodor可以更改HTTP状态码，也可以通过通过HTTP响应码重定向，选择301、302、307、308可以配置重定向地址。

### Mock
主要用于某个特定的请求返回指定的内容，您可以理解为一个本地的HTTP服务器，对匹配上的请求返回设定好的内容。  

  
***写在最后：由于HTTP协议的传输控制有非常多的组合方式，作者在测试时难免有考虑不周的地方，如果你发现某个功能没有按照文档的描述运作，或者说没有达到您的预期结果，请通过email联系我们`hodorsoft@outlook.com`。创作不易，如果您觉得用起来顺手，希望去AppStore给个好评，你的支持是我更新的最大动力。***
