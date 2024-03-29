### TCP粘包处理

Hodor提供几种TCP在传输过程中几种常见的粘包处理器，即便更准确的捕获数据包并记录

#### NotSpecified
TCP拆包协议未指定时，将按照TCP每次发送或接收进行数据的记录和重写，这有可能导致粘包的出现，因为系统在发送TCP数据时可能会对一次发送的数据拆分成多次发送，也可能将多次发送合并为一次发送，因此如果要对TCP协议进行重写，最好明确知道TCP所使用的拆包协议，如果指定的协议和实际的不匹配，极有可能导致一些数据传输异常

#### JSONRPC

``JSONRPC`` 负责以 'Content-Length' HTTP-like 头部格式发出 JSON-RPC 无线协议，例如 LSP（语言服务器协议）。

    +---------------------+
    | Content-Length: 100 |
    +---------------------+
    | \r\n\r\n            |
    +---------------------+
    | 100 length playload |
    +---------------------+

#### FixedLength

一种解码器，按固定字节数拆分接收到的 `ByteBuffer`。例如，如果接收到以下四个片段化的数据包：

    +---+----+------+----+
    | A | BC | DEFG | HI |
    +---+----+------+----+

一个 ``FixedLength`` 解码器将将它们解码为具有固定长度的三个数据包：

    +-----+-----+-----+
    | ABC | DEF | GHI |
    +-----+-----+-----+

#### LengthField

一种解码器，按照缓冲区内包含的固定长度头部所指定的字节数拆分接收到的 `ByteBuffer`。

例如，如果接收到以下四个片段化的数据包：

    +---+----+------+----+
    | A | BC | DEFG | HI |
    +---+----+------+----+

假设指定的头部长度为 1 字节，第一个头部指定了 3 个字节，而第二个头部指定了 4 个字节，
一个 ``LengthField`` 解码器将将它们解码为以下数据包：

    +-----+------+
    | BCD | FGHI |
    +-----+------+

充当头部的 'A' 和 'E' 将不会继续传递。

#### LineBased
 
一个解码器，根据行结束字符（`'\n'` 或 `'\r\n'`）拆分传入的 `ByteBuffer`。

例如，考虑以下接收到的缓冲区：

    +----+-------+------------+
    | AB | C\nDE | F\r\nGHI\n |
    +----+-------+------------+

一个 ``LineBased`` 实例将按如下方式拆分该缓冲区：

    +-----+-----+-----+
    | ABC | DEF | GHI |
    +-----+-----+-----+
