# Script Usage Instructions

Hodor supports three types of scripts, corresponding to four JavaScript entry functions. Hodor will call the corresponding interface functions at appropriate times. You only need to write the logic you want based on the parameters of the entry function.   

The JavaScript API used by Hodor can be found in the [interface documentation](https://ximlu.github.io/global.html#onRequest).

### 1. HTTP Rewrite  
**Called before the app sends a request to the real server and before the real server responds to the app, can be used to dynamically modify HTTP requests and responses.**

- The entry function for modifying requests is `async function onRequest(context, url, request)`.
- The entry function for modifying responses is `async function onResponse(context, url, response)`.
  
Specific script examples can be found in the [interface documentation](https://ximlu.github.io/global.html#onRequest).

```
app ------ Call onRequest(context, url, request) --------> real server
app <----- Call onResponse(context, url, response) ------- real server
```

As shown in the diagram above, the `onRequest` method is synchronously called before the request is sent, with parameters (context, url, request), and the `onResponse` method is synchronously called before the response is returned to the app, with parameters (context, url, response).

### 2. HTTP Session Completed  

**Asynchronously called when the HTTP response is completed, without affecting data transmission between the app and the real server. Can be used for data collection, for example, if you want to export certain data, you can create an HTTP server yourself and then use HTTPClient in this script to pass the data to the server.**

The entry function for scripts is `async function onSessionCompleted(context, url, request, response)`, and specific script examples can be found in the [interface documentation](https://ximlu.github.io/global.html#onSessionCompleted).

```
app ------------------------------------> real server
app <------------------------------------ real server
				| 
				⇣
Call onSessionCompleted(context, url, request, response)
```

As shown in the diagram above, `onSessionCompleted` is asynchronously called after the server returns a response, with parameters (context, url, request, response).

### 3. Schedule

**Mainly used for executing scheduled tasks, relying on the design of Cron expressions, can be used to start a task at a specific time or loop through tasks, such as sending requests, etc.**

The entry function for scripts is `async function onSchedule(context)`, and specific script examples can be found in the [interface documentation](https://ximlu.github.io/global.html#onSchedule).

Hodor supports Cron expressions with 5 or 6 parts.  
The format of the 6-part expression is: ```Second``` ```Minute``` ```Hour``` ```Day of month``` ```Month``` ```Day of week```
When creating an expression, you can use this [5-part generator](https://crontab.guru) or [6-part (without year) generator](https://www.freeformatter.com/cron-expression-generator-quartz.html).  
I use [CrontabGuru](https://crontab.guru/) as a reference.  
Therefore, you can parse any expression consisting of numbers and `*`, `,`, `/`, and `-` symbols.

Here are some cron examples:

- Cron expression to execute every minute: `* * * * *`  
- Cron expression to execute every second: `* * * * * *`