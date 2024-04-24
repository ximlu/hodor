### Hodor User Manual

HTTP is a packet capture tool based on the IP protocol. Currently, the vast majority of packet capture software in the application market captures data through system HTTP proxies. However, software developed with Flutter bypasses system HTTP proxies through some technical means. Since Hodor is implemented based on the IP protocol and is lower-level, it can capture all data traffic. In addition to Flutter, many conventional packet capture tools that cannot capture traffic can also be captured through Hodor.

#### 1. Filter Usage Manual

Set some filtering rules to capture specific requests.
For detailed documentation, please refer to the [user manual](https://ximlu.github.io/hodor/record_en.html).

#### 2. Rewrite Usage Manual

Predefine rules to debug network traffic for clients or servers.
For detailed documentation, please refer to the [user manual](https://ximlu.github.io/hodor/rewrite_en.html).

#### 3. Script Usage Manual

Hodor extends some special functions using JavaScript.
For detailed documentation, please refer to the [user manual](https://ximlu.github.io/hodor/script_en.html).

#### 4. HTTP Proxy Usage Manual

You can forward system traffic to a specified HTTP proxy server for data control.
For detailed documentation, please refer to the [user manual](https://ximlu.github.io/hodor/proxy_en.html).

#### 5. Local Network Functionality Description

In a local network environment, Hodor can capture traffic from other devices (such as Android), but it cannot capture all traffic from these devices. This is because Hodor does a lot of work at a low level to capture traffic. However, Apple devices with Hodor installed can forward captured traffic to other devices in the local network using Hodor's HTTP proxy functionality.

***If you have any usage questions, you can contact us via email at [hodorsoft@outlook.com](hodorsoft@outlook.com). You can also leave a 
five-star review on the App Store. Your support is the greatest motivation for our updates.***