#NGINX 
Docs and information relating to nginx setup and configuration

####Links
[Setting Up Nginx + PHP-FPM](http://blog.frd.mn/install-nginx-php-fpm-mysql-and-phpmyadmin-on-os-x-mavericks-using-homebrew/)

[Setting Up Virtual Hosts](https://www.digitalocean.com/community/articles/how-to-set-up-nginx-virtual-hosts-server-blocks-on-ubuntu-12-04-lts--3)

[Install LEMP Stack (Linux nginx MySQL PHP)](https://www.digitalocean.com/community/articles/how-to-install-linux-nginx-mysql-php-lemp-stack-on-ubuntu-12-04)

Install nginx
    
    sudo apt-get install nginx

Start nginx

    sudo service nginx start 

Confirm nginx has started

    ifconfig eth0 | grep inet | awk { print $2 }''