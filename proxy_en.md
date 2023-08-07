### Setting Up Proxy 

#### 1. What is an HTTP Proxy?

The main function of an HTTP proxy is to forward the system's HTTP traffic to other tools in the LAN for data processing (such as Fiddler, Charles, etc.), similar to manually specifying an HTTP proxy server under the system WiFi connection. The difference is that Hodor can forward HTTP traffic that cannot be captured by the system proxy after enabling advanced mode, such as HTTP traffic of a Flutter App, If you forward the traffic to another tool for processing, the logging and rewriting functionality of the current app will be invalid.  

The essence of this feature is that you can view and modify data on your computer screen, since the computer screen is larger and more convenient for viewing, and some more advanced rewriting that Hodor does not support can also be achieved with other tools.

#### 2. Notes for Decrypting HTTPS

For HTTPS protocol, if you set up another tool as a proxy server, such as Fiddler, you need to install the root certificate created by Fiddler for decoding HTTPS requests on the current device and trust this certificate so that the HTTP proxy server has the ability to decrypt HTTPS requests.

There are many tutorials on using Fiddler to capture iOS system HTTPS requests on the internet, and the installation of the certificate is the same without any difference.

#### 3. How to Configure

Take Fiddler as an example here. First, your proxy server device and your machine need to be on the same LAN. If you have installed Fiddler on another Mac, you need to get the IP address of this Mac on the LAN and the port number listened by Fiddler. Then, simply add this IP address and the port number to the proxy configuration, select the proxy server as the target server, and it will take effect.

The configuration of this feature is similar to that of configuring Fiddler to capture HTTP requests in the iOS system, only one is configured in the settings of the iOS system, and the other is configured here.

***Finally, Due to the various combinations of transmission control in the HTTP protocol, the author may have overlooked some aspects during testing. If you find that a certain function is not working according to the documentation or does not meet your expectations, please contact us via email at `hodorsoft@outlook.com`. Writing this software was not easy, and if you find it useful, we hope you can leave a positive review on the AppStore. Your support is our greatest motivation for future updates.***
