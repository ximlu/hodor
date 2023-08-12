## Example of Modifying Data Using Regular Expressions

Regular expression rewriting supports the modification of text data. As long as you select the text option, Hodor will attempt to parse the body data as text and then use regular expressions for replacement.

### There are two ways to use regular expressions for replacement:  
**① Directly replacing the matched string (matching a segment of data and replacing that segment).**  

For example, using the regular expression `\d+` to replace the number 888 in the string `"sample":"8888eeee"`.  

**② Using group substitution (matching a segment of data, but only replacing the content within the parentheses of the regular expression).**  

For example, using the regular expression `"sample":"(.+?)"` to replace the value part `8888eeee` in the string `"sample":"8888eeee"`.  

### Examples of common scenarios (all cases are based on JSON data)

	{
	 "sessionId": 88888888,
	 "authList": [{
		"name": "Adam",
		"startTime": 1581609600000
	 }, {
		"name": "Andrew",
		"startTime": 1581609600000
	 }]
	}
	
#### 1. Replacing all matched data
Replace all numbers with 1234. Set the regular expression as `\d+` and the replacement value as 1234. The result is as follows:

	{
	 "sessionId": 1234,
	 "authList": [{
		"name": "Adam",
		"startTime": 1234
	 }, {
		"name": "Andrew",
		"startTime": 1234
	 }]
	}
	
#### 2. Replacing a specific matched data
Replace a specific part of the matched data with 1234. Set the regular expression as `\d+`, select the option to match multiple values individually, and set the corresponding index value to 1. Set the replacement value as 1234. The result is as follows:

	{
	 "sessionId": 88888888,
	 "authList": [{
		"name": "Adam",
		"startTime": 1234
	 }, {
		"name": "Andrew",
		"startTime": 1581609600000
	 }]
	}


#### 3. Replacing matched group data (i.e., replacing the matched values within the parentheses of the regular expression)
Replace the value of name with ====. Set the regular expression as `"name": "(.*?)",` and the replacement value as ====. Select the option to replace all matches. The result is as follows:

	{
	 "sessionId": 88888888,
	 "authList": [{
		"name": "====",
		"startTime": 1581609600000
	 }, {
		"name": "====",
		"startTime": 1581609600000
	 }]
	}


#### 4. Replacing multiple matched group data (simultaneously replacing multiple group values)
Set multiple groups in a single regular expression for replacement. For example, replace all name with ==== and replace startTime with 1234. Set the regular expression as `"name": "(.*?)",[\s\S]*?"startTime": (\d+)`. Set the replacement value as two lines: ==== on the first line and 1234 on the second line. The result is as follows:

	{
	 "sessionId": 88888888,
	 "authList": [{
		"name": "====",
		"startTime": 1234
	 }, {
		"name": "====",
		"startTime": 1234
	 }]
	}

### Explanation of Regular Expression Parameters:

* Optional parameters: Regular expression replacement is based on the NSRegularExpression framework. For specific usage, you can refer to the [documentation](https://developer.apple.com/documentation/foundation/nsregularexpression/options).

* Matching scope: When matching, you can choose the matching range of the regular expression. `location` is the starting position of the string, and `length` represents the length after the starting position.

* Replacing all matches when replacing values: This means that when your regular expression matches multiple data, all matched data will be replaced in sequence.

* Replacing individually when replacing values: This means that when your regular expression matches multiple data, the corresponding data will be replaced based on the array index you provide.
