
### Decode and Modify as multipart/form-data

HTTP multipart/form-data is a data format consisting of multiple parts, often used for client-server requests with file uploads.

In the multipart/form-data data format, each form item consists of an independent part, with parts separated by a boundary. Each part can include a header with associated content, such as text, binary data, etc. The headers usually contain keywords such as Content-Disposition and Content-Type to describe the type, name, and encoding of the part, and the body is the actual data carried.

The following is an example of a multipart/form-data data format:

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
    
The above example shows a multipart/form-data request containing two form items: text and image. The text form item is plain text, whereas the image form item contains a file named example.png. The text and file data are located in different parts, with each part having its own content-type, name, and body content.

When rewriting, name and filename in the rewrite rules correspond to the Content-Disposition's name and filename. Hodor only supports the modification of name and corresponding content.
