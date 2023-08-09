### 通过KeyPath方式修改数据

KeyPath的核心逻辑，字典路径访问使用`.`，数组路径访问使用`[number]`或者`[*]`，以下示例均使用此JSON数据基础更改

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

#### 1. 修改字典的数据
将result中的code值更改为error，这里全部为字典访问可以将KeyPath设置为`result.code`, 值设置为error，数据类型选择string或者auto（auto时数据会被转换为原数据类型），得到的结果如下

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

#### 2. 修改数组里的某个数据的值
将authList中的第2个name替换为AAAAA，这里authList为数组，前后均为字典，可以将KeyPath设置为`detail.authList[1].name`, 值设置为AAAAA，数据类型选择string或者auto（auto时数据会被转换为原数据类型），得到的结果如下

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

#### 3. 修改数组里的所有数据的值

将authList中的所有的name替换为AAAAA，这里authList为数组，前后均为字典，可以将KeyPath设置为`detail.authList[*].name`, 值设置为AAAAA，数据类型选择string或者auto（auto时数据会被转换为原数据类型），得到的结果如下

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
