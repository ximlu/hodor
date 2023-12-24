### About Script Types

Hodor supports three types of scripts:

##### 1. HTTP Rewrite  
Called before sending a request and returning a response during an HTTP session, mainly used to dynamically modify requests and responses. Please refer to the documentation for specific usage of scripts.
	
##### 2. HTTP Session Completed  
  Called when an HTTP session is completed, and can be used for data collection. For example, if you want to export some data, you can create an HTTP server and use HTTPClient in this script to pass the data to the server. Please refer to the documentation for specific usage of scripts.
  
##### 3. Schedule  
 Mainly used to execute scheduled tasks, relying on the design of cron expressions, it can be used to start a task at a certain moment, such as sending requests, etc. Please refer to the documentation for specific usage of scripts.

