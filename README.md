# php-fpm-guard
Php-fpm-guard is a minimal bash daemon like service. It checks all the php-fpm servers on own machine, and if any php-fpm service is too slow (able freezing) or response with error, restarts it,
write log to self logfile, and stores php-fpm status in individual file.

Php-fpm-guard is not a real service, it is a simple bash script. It runs in background. It manadges itself.

Php-fpm-guard checks two php-fpm anomalies with a special minimal ping request:
1. php-fpm service response is too slow
2. php-fpm service response is invalid (error)

Enable the php-fpm status in php-fpm.conf file for each service:
```
    pm.status_path = /status
```
Define a minimal /ping request's response in php-fpm.conf file for each service.
```
    ping.path=/ping
    ping.response=pong
```

### 1.) Php-fpm Service Response Is Too Slow
Php-fpm-guard checks all php-fpm services in every 10 seconds. It sends a very minimal request to a php-fpm server (/ping). 

If the response time is bigger than 4 seconds, then php-fpm-guard 
- restarts the php-fpm server
- writes message to the php-fpm log file
- write /status response content into the pfg subdirectory

If the response time bigger than 6 seconds, php-fpm-guard do not wait too.

If the response time less than 5 seconds, but it more than 3 seconds, php-fpm-guard only writes message to the php-fpm log file.

### 2.) Php-fpm invalid response
The /ping request response is fix if the php-fpm service works perfectly.

If the /ping response differs from the standard (sotred in bash script), it 
- writes message to the php-fpm log file
- write /status response content into the pfg subdirectory

Currently even not restart if. It is under construction.
