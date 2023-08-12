### 解码成multipart/form-data重写

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
