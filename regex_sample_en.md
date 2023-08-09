###Modifying Text Data with Regular Expressions

Regular expression rewriting is the process of converting body data to text and then using rules to perform replacements.

Regular expressions support two types of replacements:  
**①Directly replace the string matched by the regular expression (match a piece of data and replace that data).**  
**②Replace the matched group using group method (match a piece of data, but only replace part of its content).**

Here are some commonly used examples (all examples are based on a JSON data):

    {
        "sessionId": 88888888,
        "hasVIP": false,
        "authList": [{
            "name": "Adam",
            "isValid": false,
            "startTime": 1581609600000
        }, {
            "name": "Andrew",
            "isValid": false,
            "startTime": 1581609600000
        }]
    }
    
#### 1. Replace all matched data
Replace all matching data by setting the regular expression to `\d+` and the replacement value to `000000000`. The result will be:

    {
        "sessionId": 000000000,
        "hasVIP": false,
        "authList": [{
            "name": "Adam",
            "isValid": false,
            "startTime": 000000000
        }, {
            "name": "Andrew",
            "isValid": false,
            "startTime": 000000000
        }]
    }
    
#### 2. Replace a matching data separately
To replace a specific matching data, set the regular expression to `\d+`, choose to match multiple values and set the index to `1`. Then, set the replacement value to `000000000`. The result will be:

    {
        "sessionId": 88888888,
        "hasVIP": false,
        "authList": [{
            "name": "Adam",
            "isValid": false,
            "startTime": 000000000
        }, {
            "name": "Andrew",
            "isValid": false,
            "startTime": 1581609600000
        }]
    }


#### 3. Replace the matched grouped data (i.e. replace the matching values in the regular expression parentheses)

To replace a matching group data, set the regular expression to `"name": "(.*?)",` and the replacement value to `Anla`. Choose to replace all matches. The result will be:

    {
        "sessionId": 88888888,
        "hasVIP": false,
        "authList": [{
            "name": "Anla",
            "isValid": false,
            "startTime": 1581609600000
        }, {
            "name": "Anla",
            "isValid": false,
            "startTime": 1581609600000
        }]
    }


#### 4. Replace multiple matched group data (replace multiple group values at once)

Set multiple groups and replace them in a regular expression, such as replacing all names with Anala and startTime with 000000. Set the regular expression to `"name": "(.*?)",[\s\S]*?"startTime": (\d+)`, the replacement value should be set with a newline character. The first line is `Anala`, and the second line is `0000000`. The results obtained are as follows "

    {
        "sessionId": 88888888,
        "hasVIP": false,
        "authList": [{
            "name": "Anla",
            "isValid": false,
            "startTime": 0000000
        }, {
            "name": "Anla",
            "isValid": false,
            "startTime": 0000000
        }]
    }



