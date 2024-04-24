### Packet Capture Related Knowledge

#### 1. Why can Hodor capture Flutter traffic while other packet capture software cannot?

Most packet capture software in the application market captures traffic through system HTTP proxies. However, some software like Flutter bypasses system HTTP proxies using various technical means. Hodor, being implemented based on the IP protocol and operating at a lower level, can capture all data traffic. Apart from Flutter, many native apps also bypass system HTTP proxies. But with Hodor, all HTTP traffic can be captured.

#### 2. What is the CONNECT protocol, and why do I see many CONNECT requests in my records?

The CONNECT protocol is used to establish tunnel connections between clients and servers, commonly used for SSL/TLS encrypted communication and proxy servers. Through this protocol, clients can communicate directly with target servers, and HTTPS traffic that cannot be decrypted appears as CONNECT requests.

#### 3. Why do I still see CONNECT requests even after enabling MITM?

MITM decryption only supports generic SSL/TLS. If the client performs strong certificate validation, decryption is not possible, and such requests are recorded as CONNECT requests.

#### 4. It's essential to understand the components of a URL for effective use of Hodor for packet capture.

URL (Uniform Resource Locator) is an address used to identify the location of resources on the internet. It consists of several parts:

- `scheme`: Specifies the protocol used to access the resource, such as HTTP, HTTPS, FTP, etc.
- `host`: Specifies the domain name or IP address of the server.
- `port`: Specifies the port number on which the server provides the service. If not explicitly specified, the default port is used.
- `path`: Specifies the specific path of the resource on the server, starting with a slash (/).
- `query`: Additional information parameters passed in the URL, starting with a question mark (?), multiple parameters are connected with &, represented as key-value pairs.

For example:

	http://example.com:8080/path/to/resource?foo=bar&foo1=bar1

- Scheme is `HTTP`.
- Host is `example.com`.
- Port is `8080`.
- Path is `/path/to/resource`.
- Query parameters are `foo=bar&foo1=bar1`.

These components are separately matched when matching URLs.

***If you have any usage questions, you can contact us via email at [hodorsoft@outlook.com](hodorsoft@outlook.com). You can also leave a five-star review on the App Store. Your support is the greatest motivation for our updates.***