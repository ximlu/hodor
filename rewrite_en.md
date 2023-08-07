### Rewrite Rules

Rewrite rules consist of two parts: `matching rules` (which requests to perform rewrites on) and `rewrite rules` (how to rewrite them).

### Host Rewrite

Host rewrite is used to change the target address and port number of a request, and to determine whether to use SSL/TLS encryption. This type of rule is very useful for frequent switching between test and production server addresses during testing.

### Path Rewrite

HTTP path refers to the part of the HTTP URL after the hostname, which is used to identify the path of the resource location on the web server.

    https://example.com/api/user?name=john&age=25
    
In this example, `/api/user` is the path, which usually begins with a `/`. When rewriting the path, you need to replace the entire path, and the rule you fill in must also begin with a `/`. If you want to replace the path with an empty string, simply fill in `/`.

### Query Rewrite

HTTP query is a technique for passing data through a URL, allowing parameters and values to be passed through the URL of an HTTP request using the "?" symbol. A query consists of one or more key-value pairs separated by the "&" symbol.

For example, the following URL contains a query string with two parameters (name and age):

    https://example.com/api/user?name=john&age=25

In this example, `name=john&age=25` is the query string, which is a series of key-value pairs separated by "&". When rewriting, Hodor will parse the query into key-value pairs similar to a dictionary (in reality, it's more complicated because it has to handle order and array situations), and then modify the corresponding keys and values. Additionally, these parameter names and values should be URL encoded. For example, "value 1" will be encoded as "value%201". However, Hodor will automatically handle these conversions for you, so you don't need to do any extra processing.

### Header Rewrite

HTTP Header is a set of key-value pairs, and you can add or delete certain values to the HTTP Header. However, there are several fields that need special handling, including Range, Content-Range, Content-Length, Content-Encoding, Content-Transfer-Encoding, and Transfer-Encoding. These fields are controlled by the system and will not be affected by manual entries. If you fill in the Content-Type, it will override the system's mime-type setting.

### Body Rewrite

HTTP Body can be encoded in many different ways. Hodor supports three encoding methods to modify key-value pairs: JSON, x-www-form-urlencoded, and multipart/form-data. Of course, you can also replace the entire body part dynamically. You only need to prepare the data in advance, and when the corresponding request is matched, Hodor will replace the body.

#### Decode and Modify as JSON

JSON rewriting works by matching the KeyPath and replacing or adding the Value, or deleting the corresponding Key and Value.

##### 1. What is KeyPath?
JSON modification can replace or delete a value by means of a KeyPath.  
KeyPath represents a JSON access path string designed using the keywords ".", "*", "[]", with "." used for dictionary extraction, "*" and "[]" used for array extraction.

    {
     "A": "a1", 
     "B": {
        "B1": "bbbb", // String type
        "B2": 110  // Int type
     }, 
     "C": [{
            "C1": "cccc"
        }, 
        {
            "C1": "ccccc"
        }]
    }

For example, if you want to access the value of B2, your KeyPath should be like this:
`B.B2`  
If you want to access the value of the first C1, your KeyPath should be like this:
`C[0].C1`  // where 0 is the array index
If you want to locate all C1, your KeyPath should be like this:
`C[*].C1` // where * is a wildcard, matching all content in the array

##### 2. JSON-encoded data has types, so the data type of the corresponding value should be specified when modifying the data.
*auto type*  
If the value type you set is auto, then the value will be automatically converted to the same data type as the original value. If the type conversion fails, an exception will be thrown and stored in the rewrite log. If there is no original value, it will be converted to a String type and inserted into the corresponding location.  
For example, if you want to replace the value of B2, the KeyPath should be set to `B.B2`, and the value you set should be `900`, with the data type set to `auto`. Then, this data will be automatically converted to an Int type.  

*Specified value data type*  
If you specify the data type of the modified value, then when adding or replacing the value, the value you set will be converted to the data type you specify before adding or replacing the corresponding value. Similarly, if the type conversion fails, an exception will be thrown and stored in the rewrite log.

#### Decode and Modify as x-www-form-urlencoded

x-www-form-urlencoded rewriting is decoded into key-value pairs and works by matching Keys, replacing or adding Values, or deleting corresponding Keys and Values.

Specifically, in x-www-form-urlencoded, each parameter of the request is represented as "key=value", with different parameters separated by the "&" symbol. For example:

    name=value1&age=value2&address=value3

These parameter names and values need to be URL encoded, for example, "value 1" will be encoded as "value%201". When rewriting, you don't need to manually process URL encoding, as the system will handle it automatically.

#### Decode and Modify as multipart/form-data

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

### Code Rewrite

Hodor can change HTTP status codes and redirect through HTTP response codes. You can choose 301, 302, 307, and 308 codes to configure the redirect address.

### Mock

Mock is mainly used to return specific content for a particular request. You can understand it as a local HTTP server that returns set content for matched requests.

***Finally, Due to the various combinations of transmission control in the HTTP protocol, the author may have overlooked some aspects during testing. If you find that a certain function is not working according to the documentation or does not meet your expectations, please contact us via email at `hodorsoft@outlook.com`. Writing this software was not easy, and if you find it useful, we hope you can leave a positive review on the AppStore. Your support is our greatest motivation for future updates.***
