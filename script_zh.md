# 脚本使用说明

Hodor支持3种脚本类型，对应了4个JavaScript的入口函数，Hodor会在合适的时间调用对应的接口函数，您仅需要根据入口函数的参数编写您想要的逻辑即可。  

Hodor所用到的JavaScript的API您可以[点击并查看接口文档](hhttps://ximlu.github.io/global.html#onRequest)。

### 1、HTTP Rewrite  
**在app向real server发送请求前以及real server向app返回响应前调用，可用于动态修改HTTP请求以及HTTP响应**

修改请求的入口函数为`async function onRequest(context, url, request)`  
修改响应的入口函数为`async function onResponse(context, url, response)`  
脚本具体的代码示例使用可以[查看接口文档](hhttps://ximlu.github.io/global.html#onRequest)。  

	app ------ Call onRequest(context, url, request) --------> real server
	app <----- Call onResponse(context, url, response) ------- real server

从上图你可以看到，在请求发送前会同步调用`onRequest`方法，并且参数有(context, url, request)，在响应返回app前会同步调用`onResponse`方法，并且参数有(context, url, response)  


### 2、HTTP Session Completed  

**在HTTP响应完成时异步调用，不影响app和real server之间的数据传输。可用于数据的采集，比如你想将某些数据导出，你可以自建一个HTTP服务器，然后在此脚本中使用HTTPClient将数据传递到服务器。**  

脚本入口函数为`async function onSessionCompleted(context, url, request, response)`，脚本具体的代码示例使用可以[查看接口文档](https://ximlu.github.io/global.html#onSessionCompleted)。

	app ------------------------------------> real server
	app <------------------------------------ real server
				| 
				⇣
	Call onSessionCompleted(context, url, request, response)

从上图你可以看到，在服务器返回响应后，会异步调用`onSessionCompleted`方法，并且参数有(context, url, request, response)

### 3、Schedule

**主要是用于执行定时任务，依赖Cron表达式的设计，可以用来在某个时刻启动一个任务, 或循环执行任务，比如发送一些请求等。**  

脚本入口函数为`async function onSchedule(context)` ，脚本具体的代码示例使用可以[查看接口文档](https://ximlu.github.io/global.html#onSchedule)。

Hodor支持5个或6个部分的Cron表达式。  
6个部分的格式是：```Second``` ```Minute``` ```Hour``` ```Day of month``` ```Month``` ```Day of week```
创建表达式时，你可以使用这个[5个部分](https://crontab.guru) 或 [6个部分（不支持年份）](https://www.freeformatter.com/cron-expression-generator-quartz.html) 生成器  
我使用 [CrontabGuru](https://crontab.guru/) 作为参考  
因此，你可以解析任何由数字和 `*` `,` `/` 和 `-` 符号组成的表达式   

一些cron示例：  

- 一分钟执行一次Cron表达式  `* * * * *`  
- 一秒执行一次Cron表达式  `* * * * * *`