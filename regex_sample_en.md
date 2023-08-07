### Capture Knowledge

#### 1. Why can Hodor capture Flutter traffic while other capture software cannot?

This is because capture software on the app market uses system HTTP proxies to forward traffic, while some applications such as Flutter use techniques to bypass the system HTTP proxies. However, Hodor is implemented based on the IP protocol, which is lower-level, hence it can capture all data traffic. In addition to Flutter, many native apps also bypass system HTTP proxies, but if you use Hodor, all HTTP traffic can be captured.

#### 2. What is the CONNECT protocol, and why are there so many CONNECT requests in my records?

The CONNECT protocol is a protocol for establishing tunnel connections between the client and server, typically used for SSL/TLS encrypted communication and proxy servers. Using this protocol, the client can communicate directly with the target server. In short, the system converts the encrypted HTTPS traffic into a CONNECT protocol. When the proxy server receives the CONNECT protocol, it will forward the corresponding traffic directly without being concerned about its content. Therefore, if you do not decrypt data traffic using MITM, you will only see CONNECT requests.

In Hodor, if you enable advanced mode, it captures TCP traffic and converts it to a CONNECT request to forward to the proxy server. Therefore, if you want to view TCP traffic, you can pay attention to the CONNECT request of the corresponding domain name.

#### 3. Why do some requests still show CONNECT even though I have enabled MITM?

This is because MITM decryption supports only one-way authentication, that is, the client authenticates the server. If two-way authentication is adopted, that is, both the client and server need to be authenticated, it cannot be decrypted. Requests that cannot be decrypted will be recorded as CONNECT requests.

#### 4. To use Hodor capture skillfully, you must understand the components of the URL.

A Uniform Resource Locator (URL) is an address used to identify the location of a resource on the Internet. It consists of several parts:

`scheme`: specifies the protocol used to access the resource, such as HTTP, HTTPS, FTP, etc.  
`host`: specifies the domain name or IP address of the server.  
`port`: specifies the port number on which the server provides the service, and if not explicitly specified, the default port number is used.  
`path`: specifies the specific path of the resource on the server, starting with a forward slash /.  
`query`: passes additional information parameters in the URL, starting with a question mark ?, multiple parameters are connected by &, combined as key-value pairs.  

Examples:

	 http://example.com:8080/path/to/resource?foo=bar&foo1=bar1

`scheme` is `HTTP`  
`host` is `example.com`  
`port` is `8080`  
`path` is `/path/to/resource`  
`query` parameters are `foo=bar&foo1=bar1`  
For matching, these components are independently used for matching.

***Finally, Due to the various combinations of transmission control in the HTTP protocol, the author may have overlooked some aspects during testing. If you find that a certain function is not working according to the documentation or does not meet your expectations, please contact us via email at `hodorsoft@outlook.com`. Writing this software was not easy, and if you find it useful, we hope you can leave a positive review on the AppStore. Your support is our greatest motivation for future updates.***
