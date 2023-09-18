## TCP or WebSocket Modification

### Decoding and Rewriting as Text

If the transmitted content is text, it can be directly converted to text. In this case, use regular expressions to replace the corresponding values. The specific usage of regular expressions can refer to the regular expression rewriting in the HTTP rewriting section.

### Decoding and Rewriting as Binary

The encoding part of TCP and WebSocket uses binary transmission. Therefore, when modifying, Hodor will convert the binary data to Hex16 for data manipulation, and then restore it to binary data after modification.

For example, I have a JSON file:

`{"id":10001,"name":"Anla","age":25}`

We want to change the name to Emma:

`{"id":10001,"name":"Emma","age":25}`

After converting to hex, it becomes:

`7B226964223A31303030312C226E616D65223A22456D6D61222C22616765223A32357D`

`"name":"Anla"` converts to hex16 as `226E616D65223A22416E6C6122`

`"name":"Emma"` converts to hex16 as `226E616D65223A22456D6D6122`

Therefore, when rewriting, you can set the regular expression to `226E616D65223A22416E6C6122`, and the value replacement should be set to `226E616D65223A22456D6D6122`.

### Explanation of Regular Expression Parameters:

- Optional parameters: The regular expression replacement is based on the system framework NSRegularExpression. For specific usage, you can refer to the [documentation](https://developer.apple.com/documentation/foundation/nsregularexpression/options).

- Matching range: When matching, you can choose the matching range of the regular expression. `location` represents the starting position of the string, and `length` represents the length after the starting position.

- Replace all matches when replacing values: When your regular expression matches multiple data, it will replace all matches one by one.

- Replace individually when replacing values: When your regular expression matches multiple data, it will replace the corresponding data based on the array index you provided.