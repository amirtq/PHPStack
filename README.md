# PHPStack

## What is PHPStack,
A simple and tiny docker-compose to run Apache2, NGINX, PHP-FPM and MariaDB+PHPMyadmin



## How to run,
### Run in normal mode
- Clone the repo and run 'docker-compose up' in terminal
### Run in daemon mode
- Clone the repo and run 'docker-compose up -d' in terminal



## How to use,

### WWW root,
- There is a folder named wwwroot in the compose root folder, it will be mounted as /var/www/ to the NGINX and Apache2 containers.
Both NGINX and Apache2 will have access to the wwwroot same as each other and at a same time, so you can test your code with both web servers in parallel.