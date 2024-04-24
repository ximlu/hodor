### URLScheme

URLScheme 可以用于通过其他应用程序控制Hodor，或创建快捷指令。

#### 启动抓包

例如:

```hodor://open?record=true&rewrite=true```

| 参数 | 可选值 | 描述 |
| --- | --- | --- |
| record | true 或 false | 启用或禁用数据包抓包功能 |
| recordrule | 抓包规则名称 | 根据名称切换到相应的抓包规则 |
| rewrite | true 或 false | 启用或禁用重写功能 |
| rewriterule | 重写规则名称 | 根据名称切换到相应的重写规则 |
| proxy | 主机:端口 | 根据主机地址和端口号切换到相应的代理服务器 |
| lan | true 或 false | 启用或禁用本地网络数据包抓包功能 |

#### 关闭抓包

```hodor://shutdown``` 


***如果您有任何使用问题，可以通过email联系我们[hodorsoft@outlook.com](hodorsoft@outlook.com)，也可以在App Store给个五星好评，您的支持是我更新的最大动力。***