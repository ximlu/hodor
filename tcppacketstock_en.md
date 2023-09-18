### TCP

#### NotSpecified

When the TCP packet splitting protocol is not specified, the data will be recorded and rewritten based on each TCP send or receive operation. This may lead to the occurrence of packet sticking, as the system may split the data from a single send operation into multiple sends, or combine multiple sends into one. Therefore, if rewriting the TCP protocol, it is best to have a clear understanding of the packet splitting protocol used by TCP. Mismatch between the specified protocol and the actual protocol can highly likely result in abnormal data transmission.

#### JSONRPC 

``JSONRPC`` is responsible for emitting JSON-RPC wire protocol with 'Content-Length'
HTTP-like headers as used by for example by LSP (Language Server Protocol).

    +---------------------+
    | Content-Length: 100 |
    +---------------------+
    | \r\n\r\n            |
    +---------------------+
    | 100 length playload |
    +---------------------+

#### FixedLength 

A decoder that splits the received `ByteBuffer` by a fixed number
 of bytes. For example, if you received the following four fragmented packets:

    +---+----+------+----+
    | A | BC | DEFG | HI |
    +---+----+------+----+

A ``FixedLength`` will decode them into the
 following three packets with the fixed length:

    +-----+-----+-----+
    | ABC | DEF | GHI |
    +-----+-----+-----+

#### LengthField

A decoder that splits the received `ByteBuffer` by the number of bytes specified in a fixed length header
 contained within the buffer.

 For example, if you received the following four fragmented packets:

    +---+----+------+----+
    | A | BC | DEFG | HI |
    +---+----+------+----+

 Given that the specified header length is 1 byte,
 where the first header specifies 3 bytes while the second header specifies 4 bytes,
 a ``LengthField`` will decode them into the following packets:

    +-----+------+
    | BCD | FGHI |
    +-----+------+

 'A' and 'E' will be the headers and will not be passed forward.

#### LineBased

A decoder that splits incoming `ByteBuffer`s around line end
 character(s) (`'\n'` or `'\r\n'`).

 Let's, for example, consider the following received buffer:

    +----+-------+------------+
    | AB | C\nDE | F\r\nGHI\n |
    +----+-------+------------+

 A instance of ``LineBased`` will split this buffer
 as follows:

    +-----+-----+-----+
    | ABC | DEF | GHI |
    +-----+-----+-----+
