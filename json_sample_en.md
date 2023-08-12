### Modifying JSON Data Using KeyPath

KeyPath access in JSON is a way to access nested properties of an object using dot notation (`.`). Hodor uses dots to separate KeyPath into a group of property names, and then retrieves values based on these property names. KeyPath also supports array access using `[index]` or `[*]`, where `index` refers to a specific array index and `*` acts as a wildcard.

### Example Usage
We will provide a sample JSON data for better understanding. The sample data is as follows:

```json
{
 "detail": {
 	"sessionId": 88888888,
 	"hasVIP": false,
 	"authList": [{
 	 "name": "Adam",
 	 "startTime": 1581609600000
 	}, {
 	 "name": "Andrew",
 	 "startTime": 1581609600000
 	}]
 },
 "result": {
 	"code": "ok",
 	"updateTime": 1667573961226
 }
}
```

#### 1. Modifying data in a deeply nested dictionary
How can we change the value of `code` in `result` to "error"?

Since this is a dictionary access, the KeyPath can be set as `result.code` and the value can be set as "error". You can choose either string or auto as the data type (auto converts the data to its original data type). The resulting JSON will be:

```json
{
  "detail" : {
    "authList" : [{
        "name" : "Adam",
        "startTime" : 1581609600000
      },
      {
        "name" : "Andrew",
        "startTime" : 1581609600000
      }],
    "sessionId" : 88888888,
    "hasVIP" : false
  },
  "result" : {
    "code" : "error",
    "updateTime" : 1667573961226
  }
}
```

#### 2. Modifying the value of an element in an array
How can we replace the value of the second `name` in `authList` with "AAAAA"?

Since `authList` is an array, and both ends are dictionaries, the KeyPath can be set as `detail.authList[1].name` and the value can be set as "AAAAA". You can choose either string or auto as the data type (auto converts the data to its original data type). The resulting JSON will be:

```json
{
  "detail" : {
    "sessionId" : 88888888,
    "hasVIP" : false,
    "authList" : [{
        "name" : "Adam",
        "startTime" : 1581609600000
      },
      {
        "name" : "AAAAA",
        "startTime" : 1581609600000
      }]
  },
  "result" : {
    "updateTime" : 1667573961226,
    "code" : "ok"
  }
}
```

#### 3. Modifying the value of all elements in an array
How can we replace the value of all `name` in `authList` with "AAAAA"?

Since `authList` is an array, the KeyPath can be set as `detail.authList[*].name` and the value can be set as "AAAAA". You can choose either string or auto as the data type (auto converts the data to its original data type). The resulting JSON will be:

```json
{
  "detail" : {
    "authList" : [{
        "name" : "AAAAA",
        "startTime" : 1581609600000
      },
      {
        "name" : "AAAAA",
        "startTime" : 1581609600000
      }],
    "hasVIP" : false,
    "sessionId" : 88888888
  },
 "result" : {
    "updateTime" : 1667573961226,
    "code" : "ok"
  }
}
```

#### 4. Modifying a bool type
How can we change `hasVIP` to true?

The KeyPath can be set as `detail.hasVIP` and the value can be set as true. You can choose either bool or auto as the data type (auto converts the data to its original data type). The resulting JSON will be:

```json
{
  "detail" : {
    "authList" : [{
        "name": "Adam",
        "startTime": 1581609600000
      },
      {
        "name": "Andrew",
        "startTime": 1581609600000
      }],
    "hasVIP" : true,
    "sessionId" : 88888888
  },
 "result" : {
    "updateTime" : 1667573961226,
    "code" : "ok"
  }
}
```

#### 5. Replacing a dictionary with another dictionary
How can we replace `result` with another dictionary?

In this case, the KeyPath can be set as `result` and the value can be set as `{"a" : 1,"b" : "ok"}`. You should choose dictionary as the data type (Hodor will convert the provided string to a dictionary during the replacement process). The resulting JSON will be:

```json
{
 "detail": {
 	"sessionId": 88888888,
 	"hasVIP": false,
 	"authList": [{
 	 "name": "Adam",
 	 "startTime": 1581609600000
 	}, {
 	 "name": "Andrew",
 	 "startTime": 1581609600000
 	}]
 },
 "result" : {
    "a" : a,
    "b" : "ok"
  }
}
```