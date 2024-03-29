## TCP或WebSocket修改

### 解码成text重写

如果传输内容是文本，可以直接将内容转换为文本，此时用正则表达式替换对应的值，正则表达式具体的使用可以参考HTTP重写部分的正则表达式重写。

### 解码成binary重写

TCP和WebSocket的编码部分会采用二进制传输，因此Hodor在改写时会将二进制数据转换为Hex16进行数据操作，当修改完成以后又还原成二进制数据。

例如我一个JSON文件

`{"id":10001,"name":"Anla","age":25}`

我们想把name改为Emma

`{"id":10001,"name":"Emma","age":25}`

转换成hex以后是

`7B226964223A31303030312C226E616D65223A22416E6C61222C22616765223A32357D`

`"name":"Anla"` 转换为hex16为 `226E616D65223A22416E6C6122`

`"name":"Emma"` 转换为hex16为 `226E616D65223A22456D6D6122`

因此在改写时你可以将正则表达式设置为`226E616D65223A22416E6C6122`，值替换设置为`226E616D65223A22456D6D6122`

### 正则表达式参数说明：  

* 可选参数：正则表达式替换是基于系统框架NSRegularExpression具体使用您可以查看[文档地址](https://developer.apple.com/documentation/foundation/nsregularexpression/options)  

* 匹配范围：匹配时你可以选择正则表达式的匹配区域，location是字符串的开始位置，length表示从开始位置后的长度  

* 值替换时全部匹配：即当你的正则表达式匹配到多个数据时，将依次全部替换所有匹配到的数据
* 值替换时逐个匹配：即当你的正则表达式匹配到多个数据时，会根据所填写的数组下标替换对应的数据  
  