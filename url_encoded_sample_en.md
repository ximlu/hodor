### Decode and Modify as x-www-form-urlencoded

x-www-form-urlencoded rewriting is decoded into key-value pairs and works by matching Keys, replacing or adding Values, or deleting corresponding Keys and Values.

Specifically, in x-www-form-urlencoded, each parameter of the request is represented as "key=value", with different parameters separated by the "&" symbol. For example:

    name=value1&age=value2&address=value3

These parameter names and values need to be URL encoded, for example, "value 1" will be encoded as "value%201". When rewriting, you don't need to manually process URL encoding, as the system will handle it automatically.
