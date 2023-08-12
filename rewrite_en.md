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

### Body Rewrite
The HTTP Body can be encoded in various ways. Hodor supports decoding the data into 4 encoding formats and modifying it in a key-value pair manner: text, JSON, x-www-form-urlencoded, and multipart/form-data. Of course, you can also dynamically replace the entire Body section by preparing the data in advance. When a matching request is encountered, the Body will be replaced.

#### 1. Decoding and modifying as text using regular expressions

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/regex_sample_en.html).

#### 2. Decoding and modifying as JSON

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/json_sample_en.html).

#### 3. Decoding and modifying as x-www-form-urlencoded

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/url_encoded_sample_en.html).

#### 4. Decoding and modifying as multipart/form-data

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/form_sample_en.html).

### Code Rewrite

Hodor can change HTTP status codes and redirect through HTTP response codes. You can choose 301, 302, 307, and 308 codes to configure the redirect address.

### Mock

Mock is mainly used to return specific content for a particular request. You can understand it as a local HTTP server that returns set content for matched requests.

***Finally, Due to the various combinations of transmission control in the HTTP protocol, the author may have overlooked some aspects during testing. If you find that a certain function is not working according to the documentation or does not meet your expectations, please contact us via email at `hodorsoft@outlook.com`. Writing this software was not easy, and if you find it useful, we hope you can leave a positive review on the AppStore. Your support is our greatest motivation for future updates.***
