# PHPStack

## What is PHPStack :
A simple and tiny docker-compose to run Apache2, NGINX, PHP-FPM and MariaDB+PHPMyadmin with a single command.
## What is NOT PHPStack :
PHPStack is not a good choice to change it's ports from 127.0.0.0:x to 0.0.0.0:x then use for production, to keep it easy to use, there is not any server hardening, even remote root login is enabled for MariaDB!!!



## How to run:
### Run in normal mode
- Clone the repo and run 'docker-compose up' in terminal.
### Run in daemon mode
- Clone the repo and run 'docker-compose up -d' in terminal.




## How to use:

### Web Servers
- ./wwwroot is mounted as /var/www/ to the NGINX and Apache2 containers.
Both NGINX and Apache2 will have access to the wwwroot same as each other and at a same time, so you can test your code with both web servers in parallel.

#### NGINX and PHP-FPM for NGINX
##### NGINX web server
- By default, NGINX will be available on localhost:80 for HTTP and localhost:443 for HTTPS, you can change mentioned ports by modifying the .env file however, avoid port conflict between NGINX and Apache2 else your containers will not start as expected.
- To add new virtual host, use './nginx-and-phpfpm/nginx/sites-enabled/default.conf' as sample and put it in './nginx-and-phpfpm/nginx/sites-enabled' then re-run containers or run 'systemctl reload nginx' inside of "nginx-web" container.
- To change NGINX default configuration, modify ./nginx-and-phpfpm/nginx.conf .
- To use SSL certificates, put them in './ssl-certs' and it will be available as '/ssl-certs' in the "nginx-web" container. The default code includes a self-signed certificate for *.phpstack.local .

##### PHP-FPM for NGINX
- For NGINX, there is a separated container named "nginx-phpfpm". It will serve NGINX for PHP processing using TCP 9000, you can find the sample configuration file in ./nginx-and-phpfpm/nginx/sites-enabled/default.conf' .
- to change PHP configurations, there is an .ini file in './nginx-and-phpfpm/php-fpm/extra.ini' .
- Many PHP extensions are included in the code, however, if you need to add more extensions like ioncube, use mentioned .ini file and put your extension files in './nginx-and-phpfpm/php-fpm/extra-extensions' and it will be available as '/usr/local/lib/php/extensions/extra-extensions' in the "nginx-phpfpm" container.
- For PHP cronjobs, write your cron tasks in the './nginx-and-phpfpm/php-fpm/cronjobs' and after about 3 minutes, it will be automatically loaded into the "nginx-phpfpm" crontab.

#### Apache2 and PHP-FPM for Apache2 (Both in a single container named "apache2-with-phpfpm")
##### Apache2 web server
- By default, Apache2 will be available on localhost:880 for HTTP and localhost:8443 for HTTPS, you can change mentioned ports by modifying the .env file however, avoid port conflict between Apache2 and NGINX else your containers will not start as expected.
- To add new virtual host, use './apache2-and-phpfpm/sites-enabled/default.conf' as sample and put it in './apache2-and-phpfpm/sites-enabled/sites-enabled' then re-run containers or run 'systemctl reload apache2' inside of "apache2-with-phpfpm" container.
- To change Apache2 default configuration, modify ./apache2-and-phpfpm/apache2.conf .
- To use SSL certificates, put them in './ssl-certs' and it will be available as '/ssl-certs' in the "apache2-with-phpfpm" container. The default code includes a self-signed certificate for *.phpstack.local .
##### PHP-FPM for Apache2
- To change PHP configurations, there is an .ini file in './apache2-and-phpfpm/php-extra.ini' .
- Many PHP extensions are included in the code, however, if you need to add more extensions like ioncube, use mentioned .ini file and put your extension files in './apache2-and-phpfpm/php-extra-extensions' and it will be available as '/usr/local/lib/php/extensions/extra-extensions' in the "apache2-with-phpfpm" container.
- For PHP cronjobs, write your cron tasks in the './apache2-and-phpfpm/cronjobs' and after about 3 minutes, it will be automatically loaded into the "apache2-with-phpfpm" crontab.


### Database Servers
#### MariaDB (MySQL) Server and PHPMyadmin
- PHPMyadmin will be available on http://localhost:8080 , you can change mentioned ports by modifying the .env file.
- MariaDB will be available to containers with server name "mariadb-10.7" on port "TCP 3306", you can change mentioned ports by modifying the .env file.
- Data of the MariaDB including Schema and User databases wil be saved in ./mariadb/data .
- To change MariaDB configurations, modify './mariadb/conf.d/50-server.cnf' then re-run containers or run 'systemctl restart mariadb' inside of "mariadb-10.7" container.

