# API

Viewing log files through API calls.

If you are developing an API service, powered by CodeIgniter, this library can still be used to view your log files.

## Use

Query: ```/logs?api=list```


Response:

```json
{
   "status": true,
   "log_files": [
       {
           "file_b64": "bG9nLTIwMTgtMDEtMTkucGhw",
           "file_name": "log-2018-01-19.php"
       },
       {
           "file_b64": "bG9nLTIwMTgtMDEtMTcucGhw",
           "file_name": "log-2018-01-17.php"
       }
   ]
}
```

file_b64 is the base64 encoded name of the file that will be used in further operations and API calls

Query: ```/logs?api=viewf=bG9nLTIwMTgtMDEtMTcucGhw```
    
will return the logs contained in the log file specified by the f parameter.

The value of the f (f stands for file) is the base64 encoded format of the log file name. It is obtained from the /logs?api=list API call. A list of all available log files is also returned.

Response:

```json
{
    "log_files": [
        {
            "file_b64": "bG9nLTIwMTgtMDEtMTkucGhw",
            "file_name": "log-2018-01-19.php"
        },
        {
            "file_b64": "bG9nLTIwMTgtMDEtMTcucGhw",
            "file_name": "log-2018-01-17.php"
        }
    ],
    "status": true,
    "logs": [
        "ERROR - 2018-01-23 07:12:31 --> 404 Page Not Found: admin/Logs/index",
        "ERROR - 2018-01-23 07:12:37 --> 404 Page Not Found: admin//index",
        "ERROR - 2018-01-23 15:23:02 --> 404 Page Not Found: Faviconico/index"
    ]
}
```

The API Query can also take one last parameter, sline that will determine how the logs are returned When it's true the logs are returned in a single line:

Query: ```/logs?api=view&f=bG9nLTIwMTgtMDEtMTkucGhw&sline=true```

Response:

```json
{
   "log_files": [
       {
           "file_b64": "bG9nLTIwMTgtMDEtMTkucGhw",
           "file_name": "log-2018-01-19.php"
       },
       {
           "file_b64": "bG9nLTIwMTgtMDEtMTcucGhw",
           "file_name": "log-2018-01-17.php"
       }
   ],
   "status": true,
   "logs": "ERROR - 2018-01-23 07:12:31 --> 404 Page Not Found: admin/Logs/index\r\nERROR - 2018-01-23 07:12:37 --> 404 Page Not Found: admin//index\r\nERROR - 2018-01-23 15:23:02 --> 404 Page Not Found: Faviconico/index\r\n"
}
```

When it's false (Default), the logs are returned in as an array, where each element is a line in the log file:

Query: ```/logs?api=view&f=bG9nLTIwMTgtMDEtMTkucGhw&sline=false OR logs?api=view&f=bG9nLTIwMTgtMDEtMTkucGhw```

Response:

```json
{
   
   "logs": [
       "ERROR - 2018-01-23 07:12:31 --> 404 Page Not Found: admin/Logs/index",
       "ERROR - 2018-01-23 07:12:37 --> 404 Page Not Found: admin//index",
       "ERROR - 2018-01-23 15:23:02 --> 404 Page Not Found: Faviconico/index"
   ]
}
```

Query: ```/logs?api=delete&f=bG9nLTIwMTgtMDEtMTkucGhw``` 

will delete a single log file. The f parameter is the base64 encoded name of the file and can be obtained from the view api above.

Query: ```/logs?api=delete&f=all ```

will delete all log files in the configured folder path. Take note of the value for f which is the literal 'all'.

IF A FILE IS TOO LARGE (> 50MB), YOU CAN DOWNLOAD IT WITH THIS API QUERY ```/logs?dl=bG9nLTIwMTgtMDEtMTcucGhw```