# Ubuntu 16.04 安装PHP运行环境



```
sudo apt-get update 
sudo apt-get install -y language-pack-en-base
locale-gen en_US.UTF-8

sudo apt-get install software-properties-common 
sudo LC_ALL=en_US.UTF-8 add-apt-repository ppa:ondrej/php
sudo apt-get update 

//php安装
sudo apt-get -y install php7.1
sudo apt-get -y install php7.1-mysql
sudo apt-get install php7.1-fpm

apt-get install php7.1-curl php7.1-xml php7.1-mcrypt php7.1-json php7.1-gd php7.1-mbstring

//nginx安装
sudo apt-get -y install nginx

//mysql安装
sudo apt-get -y install mysql-server-5.6
```

php 配置

```
sudo vim /etc/php/7.1/fpm/php.ini  // 将cgi.fix_pathinfo=1这一行去掉注释，将1改为0

sudo vim /etc/php/7.1/fpm/pool.d/www.conf // 配置这个 listen = /var/run/php7.1-fpm.sock

sudo service php7.1-fpm restart
```

Nginx 基础配置如下

```
listen 80 default_server;
listen [::]:80 default_server ipv6only=on;

root /var/www/laravel-ubuntu/public;
index index.php index.html index.htm;

# Make site accessible from http://localhost/
server_name localhost;

location / {
    # First attempt to serve request as file, then
    # as directory, then fall back to displaying a 404.
    try_files $uri $uri/ /index.php?$query_string;
    # Uncomment to enable naxsi on this location
    # include /etc/nginx/naxsi.rules
}
location ~ \.php$ {
    try_files $uri /index.php =404;
    fastcgi_split_path_info ^(.+\.php)(/.+)$;
    fastcgi_pass unix:/var/run/php7.1-fpm.sock;
    fastcgi_index index.php;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
}
```

还有就是，注意 laravel-ubuntu 这个目录的所有者为: www-data:www-data

最后给，storage 文件夹权限，重启 Nginx

来源：https://www.codecasts.com/discuss/laravel/laravel-project-from-scratch-deployment-752