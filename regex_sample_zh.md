### 使用正则表达式修改文本数据示例

正则表达式重写是将Body数据转换为文本，然后利用规则进行替换。  

正则表达式支持2种方式的替换：  
**①直接替换正则表达式匹配到的字符串（匹配一段数据，并替换这段数据）。**  
**②使用group方式替换匹配到的group（匹配一段数据，但是只替换中间的部分内容）。**  

以下为部分常用的示例 （以下用例均基于一个JSON数据） 

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
	
#### 1. 替换所有匹配到的数据
将所有的数字替换为000000000，正则表达式设置为`\d+`, 替换值设置为000000000，得到的结果如下：

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
	
#### 2. 单独替换某个匹配到的数据
将匹配到的数据部分替换000000000，正则表达式设置为`\d+`, 多值匹配选择逐个匹配，并设置对应的index值，这里设置为1，替换值设置为000000000，得到的结果如下：

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


#### 3. 替换匹配到的分组数据（即替换正则表达式小括号中匹配的值）
将name的值替换为Anla，正则表达式式设置为`"name": "(.*?)",`，值设置为Anla，多匹配时选择全部替换，得出的结果为

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


#### 4. 替换匹配到的多个分组数据（一次性替换多个group值）
在一个正则表达式中设置多个group并替换，例如将所有name替换为Anla，同时startTime替换为0000000，正则表达式设置为`"name": "(.*?)",[\s\S]*?"startTime": (\d+)`，替换值应使用换行符设置2个值第一行为"Anla"，第二行为"0000000"，得到的结果如下

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



