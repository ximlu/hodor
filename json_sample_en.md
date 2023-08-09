### Modifying data through KeyPath

The core logic of KeyPath, dictionary path access using `.`, The array path access uses either `[number]` or `[*]`, and the following examples use this JSON data base change

    {
        "detail": {
            "sessionId": 88888888,
            "hasVIP": false,
            "authList": [{
                "name": "Adam",
                "isValid": false,
                "startTime": 1581609600000,
            }, {
                "name": "Andrew",
                "isValid": false,
                "startTime": 1581609600000,
            }]
        },
        "result": {
            "code": "ok",
            "updateTime": 1667573961226,
        }
    }

#### 1. Modifying Dictionary Data
Change the code value in the result to error, all of which are dictionary access. You can set the KeyPath to `result.code`, set the value to error, and select string or auto as the data type (when auto is used, the data will be converted to the original data type). The results are as follows

    {
      "detail" : {
        "authList" : [
          {
            "name" : "Adam",
            "isValid" : false,
            "startTime" : 1581609600000
          },
          {
            "name" : "Andrew",
            "isValid" : false,
            "startTime" : 1581609600000
          }
        ],
        "sessionId" : 88888888,
        "hasVIP" : false
      },
      "result" : {
        "code" : "error",
        "updateTime" : 1667573961226
      }
    }

#### 2. Modify the value of a certain data in an array
Replace the second name in authList with AAAAA, where authList is an array with a dictionary before and after. You can set KeyPath to `detail.authList[1].name`, value to AAAAA, and data type to string or auto (when auto is used, the data will be converted to the original data type). The results are as follows

    {
      "detail" : {
        "sessionId" : 88888888,
        "hasVIP" : false,
        "authList" : [
          {
            "name" : "Adam",
            "isValid" : false,
            "startTime" : 1581609600000
          },
          {
            "name" : "AAAAA",
            "startTime" : 1581609600000,
            "isValid" : false
          }
        ]
      },
      "result" : {
        "updateTime" : 1667573961226,
        "code" : "ok"
      }
    }

#### 3. Modify the values of all data in the array

Replace all names in the authList with AAAAA, where authList is an array with dictionaries before and after. You can set KeyPath to `detail.authList[*].name`, value to AAAAA, and data type to string or auto (when auto is used, the data will be converted to the original data type). The results are as follows

    {
      "result" : {
        "updateTime" : 1667573961226,
        "code" : "ok"
      },
      "detail" : {
        "authList" : [
          {
            "name" : "AAAAA",
            "startTime" : 1581609600000,
            "isValid" : false
          },
          {
            "name" : "AAAAA",
            "isValid" : false,
            "startTime" : 1581609600000
          }
        ],
        "hasVIP" : false,
        "sessionId" : 88888888
      }
    }
