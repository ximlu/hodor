### Hodor User Manual

HTTP is a packet capture tool based on the IP protocol. Most packet capture software in the current market captures data through system HTTP proxies. However, software developed with Flutter bypasses the system HTTP proxy through various technical means. Hodor, on the other hand, is implemented based on the IP protocol and operates at a lower level, therefore capturing all data traffic. In addition to Flutter, many native apps also bypass the system HTTP proxy, but if you use Hodor, all HTTP traffic can be captured.

#### 1. Filter User Manual

You can set some filter rules to capture specific requests.  
For more information, please refer to the [User Manual](https://ximlu.github.io/hodor/record_en.html).

#### 2. Rewriting User Manual

You can set a series of rules to debug the client or server.  
For more information, please refer to the [User Manual](https://ximlu.github.io/hodor/rewrite_en.html).

#### 3. HTTP Proxy User Manual

You can forward system traffic to a specified HTTP proxy server to better handle the data.  
For more information, please refer to the [User Manual](https://ximlu.github.io/hodor/proxy_en.html).