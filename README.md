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

#### NGINX and PHP-FPM for NGINX
##### test
- By default, NGINX will be available on localhost:80 for HTTP and localhost:443 for HTTPS, you can change mentioned ports by modifying the .env file however, avoid port conflict between NGINX and Apache2 else your containers will not start as expected.
- To add new virtual host, use './nginx-and-phpfpm/nginx/sites-enabled/default.conf' as sample and put it in './nginx-and-phpfpm/nginx/sites-enabled' then re-run containers or run 'systemctl nginx reload' inside of "nginx-web" container
- To change NGINX default configuration, modify ./nginx-and-phpfpm/nginx.conf
- To use SSL certificates, put them in './ssl-certs' and it will be available as '/ssl-certs' in the NGINX container. The default code includes a self-signed certificate for *.phpstack.local.

