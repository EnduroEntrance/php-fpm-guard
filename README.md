# php-fpm-guard
Php-fpm-guard is a minimal bash daemon like service. It checks all the php-fpm servers on own machine, and if any php-fpm sercice is too slow (able freeze) or response with error, restart it.

Php-fpm-guard is not a real service, it is a simple bash script. It runs in background. It manadges itself.

Php-fpm guard two php-fpm service anomalies:
1 - php-fpm service response is too slow
2 - php-fpm service response is error
