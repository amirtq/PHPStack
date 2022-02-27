# PHPStack

## What is PHPStack:
A simple and tiny docker-compose to run Apache2, NGINX, PHP-FPM and MariaDB+PHPMyadmin



## How to run:
### Run in normal mode
- Clone the repo and run 'docker-compose up' in terminal
### Run in daemon mode
- Clone the repo and run 'docker-compose up -d' in terminal




## How to use:

### Web Servers:
- ./wwwroot is mounted as /var/www/ to the NGINX and Apache2 containers.
Both NGINX and Apache2 will have access to the wwwroot same as each other and at a same time, so you can test your code with both web servers in parallel.

#### NGINX
- To add new virtual host, put it in './nginx-and-phpfpm/nginx/sites-enabled' then re-run containers or use 'systemctl nginx reload' inside of "nginx-web" container and use './nginx-and-phpfpm/nginx/sites-enabled/default.conf' as sample
- To change NGINX default configuration, modify ./nginx-and-phpfpm/nginx.conf
- To 
