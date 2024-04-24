# Rewrite Rules

Rewrite rules consist of two parts: `Matching Rules` (which requests to rewrite) and `Rewriting Rules` (how to rewrite).

### Redirecting Requests for "HTTP&WebSocket&TCP"

Redirection is used to change the target address and port of a request and can also determine whether to use SSL/TLS encryption. This rule is particularly useful for frequent switching between test server and production server addresses during testing.

### Rewriting Paths for "HTTP&WebSocket"

HTTP Path refers to the part of the URL after the hostname, used to identify the path of resources on the web server.

    https://example.com/api/user?name=john&age=25
    
In this example, `/api/user` is the Path, typically starting with `/`. When rewriting the Path, the entire path needs to be replaced. If you want to replace the Path with nothing, simply fill in `/`.

### Rewriting Queries for "HTTP&WebSocket"

HTTP Query is a technique for passing data through a URL, allowing parameters and values to be passed in the URL using the "?" symbol. Queries consist of one or more key-value pairs separated by "&".

For example, the following URL contains a query string with two parameters (name and age):

    https://example.com/api/user?name=john&age=25
    
In this example, `name=john&age=25` is the query string, composed of multiple key-value pairs concatenated with "&". When rewriting, Hodor parses the Query into key-value pairs (handling order and array situations) and modifies the corresponding Key, Value. Additionally, these parameter names and values need to be URL-encoded, for example, "value 1" will be encoded as "value%201". Hodor automatically handles these conversions for you.

### Rewriting Headers for "HTTP&WebSocket"

HTTP Headers are a set of key-value pairs. You can add or remove values from the HTTP Header. However, there are a few special considerations for fields such as Range, Content-Range, Content-Length, Content-Encoding, Content-Transfer-Encoding, Transfer-Encoding, which are controlled by the system and will be ineffective if manually filled in. If Content-Type is specified, it will override the system's mime-type setting.

### Modifying Body for "HTTP"

HTTP Body can transmit data in various encoding formats. Hodor supports decoding data into four encoding formats (text, JSON, x-www-form-urlencoded, multipart/form-data) and modifying them as key-value pairs. Alternatively, you can dynamically replace the entire Body section with pre-prepared data.

#### 1. Decoding as text and modifying with regular expressions

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/regex_sample_en.html).

#### 2. Decoding as JSON for modification

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/json_sample_en.html).

#### 3. Decoding as x-www-form-urlencoded for modification

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/url_encoded_sample_en.html).

#### 4. Decoding as multipart/form-data for modification

For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/form_sample_en.html).

### Replacing Body for "HTTP"

Directly replace the Body section before the App sends the request to the Server and before the Server data returns to the App.

### Rewriting Code for "HTTP"

Hodor can change HTTP status codes and can also redirect through HTTP response codes, selecting from 301, 302, 307, 308 with configurable redirection addresses.

### Mocking for "HTTP"

Mainly used to return specific content for a particular request, you can think of it as a local HTTP server that returns preset content for matching requests.

### Modifying Data for "TCP&WebSocket"

Convert TCP or WebSocket upstream and downstream data flow into strings or hex16, then use regular expressions to modify this data. For detailed documentation, please refer to the [sample document](https://ximlu.github.io/hodor/tcp_sample_en.html).

***If you have any usage questions, you can contact us via email at [hodorsoft@outlook.com](hodorsoft@outlook.com). You can also leave a five-star review on the App Store. Your support is the greatest motivation for our updates.***