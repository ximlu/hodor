### 通过KeyPath方式修改JSON数据

JSON的KeyPath访问是一种使用点分隔符`.`来访问对象嵌套属性的方式，Hodor在进行数据改写时会使用`.`将KeyPath分割成一组属性名称，然后通过这组属性名称依次取值，KeyPath也支持数组访问，使用`[index]`或者`[*]`，这里`index`为具体的数组下标，`*`为通配符。

### 使用示例
我们将提供一个JSON样本数据以便更好的理解，样本数据如下：

```json
{
  "detail": {
    "sessionId": 88888888,
    "hasVIP": false,
    "authList": [{
        "name": "Adam",
        "startTime": 1581609600000
      },
      {
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

#### 1. 修改多层嵌套字典的数据
怎么将result中的code值更改为error？

这里全部为字典访问可以将KeyPath设置为`result.code`，值设置为"error"，数据类型选择string或者auto（auto时数据会被转换为原数据类型），得到的结果如下：

```json
{
  "detail": {
    "sessionId": 88888888,
    "hasVIP": false,
    "authList": [{
        "name": "Adam",
        "startTime": 1581609600000
      },
      {
        "name": "Andrew",
        "startTime": 1581609600000
      }]
  },
  "result": {
    "code": "error",
    "updateTime": 1667573961226
  }
}
```

#### 2. 修改数组里的某个数据的值
怎么将authList中的第2个name替换为AAAAA？

这里authList为数组，前后均为字典，可以将KeyPath设置为`detail.authList[1].name`，值设置为"AAAAA"，数据类型选择string或者auto（auto时数据会被转换为原数据类型），得到的结果如下：

```json
{
  "detail": {
    "sessionId": 88888888,
    "hasVIP": false,
    "authList": [{
        "name": "Adam",
        "startTime": 1581609600000
      },
      {
        "name": "AAAAA",
        "startTime": 1581609600000
      }]
  },
  "result": {
    "code": "ok",
    "updateTime": 1667573961226
  }
}
```

#### 3. 修改数组里的所有数据的值
怎么将authList中的所有的name替换为AAAAA？

这里authList为数组，可以将KeyPath设置为`detail.authList[*].name`，值设置为"AAAAA"，数据类型选择string或者auto（auto时数据会被转换为原数据类型），得到的结果如下：

```json
{
  "detail": {
    "sessionId": 88888888,
    "hasVIP": false,
    "authList": [{
        "name": "AAAAA",
        "startTime": 1581609600000
      },
      {
        "name": "AAAAA",
        "startTime": 1581609600000
      }]
  },
  "result": {
    "code": "ok",
    "updateTime": 1667573961226
  }
}
```

#### 4. bool类型的修改
怎么将hasVIP改为true？

可以将KeyPath设置为`detail.hasVIP`，值设置为true，数据类型选择bool或者auto（auto时数据会被转换为原数据类型），得到的结果如下：

```json
{
  "detail": {
    "sessionId": 88888888,
    "hasVIP": true,
    "authList": [{
        "name": "Adam",
        "startTime": 1581609600000
      },
      {
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

#### 5. 怎么直接使用字典替换字典
怎么将result改为其他字典？

这里可以将KeyPath设置为`result`，值设置为`{"a" : 1, "b" : "ok"}`，数据类型选择dictionary（Hodor在替换过程中会将设置的字符串转换为字典），得到的结果如下：

```json
{
  "detail": {
    "sessionId": 88888888,
    "hasVIP": false,
    "authList": [{
        "name": "Adam",
        "startTime": 1581609600000
      },
      {
        "name": "Andrew",
        "startTime": 1581609600000
      }]
  },
  "result": {
    "a": 1,
    "b": "ok"
  }
}
```