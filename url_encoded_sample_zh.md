### x-www-form-urlencoded重写示例

x-www-form-urlencoded重写是解码成键值对，采用匹配Key, 替换或新增Value，或删除对应的Key以及Value的方式工作的。

具体来说，在 x-www-form-urlencoded 中，请求的每个参数都用“键=值”的形式表示，不同参数用 & 符号分隔开。例如：

	name=value1&age=value2&address=value3

这些参数名称和值都需要进行 URL 编码，例如 “value 1” 将会被编码为 “value%201”，在重写的时候您不需要手动进行URL编码处理，系统会自动为您处理。  
