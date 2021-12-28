# Ansible setup

This repository contains two Ansible Playbooks: 

1. **setup-flaskApp.yaml** - allows to run flask application on machine which was configred by this playbook

2. **setup-wp.yaml** - allows to run WordPress on machine which was configred by this playbook

<br>

## setup-flaskApp.yaml
<hr>
First part of this file (starts with `hosts: flask_node`) is a configuration for run flask application:

1. `install os packages` - install packages: python3, python3-pip, git using yum<br>
2. `sync repo` - get a git repository (*https://github.com/kingaborycka/CeneoScraper.git*) to the target place on server (*"/opt/CeneoScrapper"*)
3. `create user` - create a linux user (*CeneoScrapper*)
4. `create venv` - create a virtual environment with python3
5. `put systemd cfg` - put flask app configuration file to the target place on server (*/etc/systemd/system/CeneoScrapper.service*)
6. `start service` - start service (CeneoScrapper Application on port 8080) 

The second part (starts with `hosts: load_balancer`) is a configuration for a simple server proxy.

LAN: 172.31.0.0/20

## Server with Flask App:
public IP address: 3.71.10.1
private IP address: 172.31.17.234

## Server Proxy:
public IP address: 18.184.189.117
private IP address: 172.31.19.237

Server Proxy redirects all calls to the server with running Flask App (172.31.17.234:8080)

<br>

![Flask App](/files/images/flask.jpg "Flask App")

<br>

## setup-wp.yaml
<hr>
First part of this file (starts with `hosts: wp_nodes`) is a configuration for run flask application, the second part (starts with `hosts: load_balancer`) is an appendix - configuration for simple proxy server. We will focus only on this first part installation steps:

1. `copy mariadb repo cfg` - get MariaDb repository
2. `install mariadb` - install MariaDb using yum
3. `reload mariadb` - start MariaDb
4. `install mysql related module` - install MySQL-python using yum
5. `create wp's db` - create a database
6. `create user && asign privileges` - create a user for the database
7. `apache is installed` - install apache using yum
8. `Config apache`- put apache configuration file to the target place on server (*/etc/httpd/conf.d/blog.conf*)
9. `EPEL installed` - install EPEL using yum (*from https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm*)
10. `Php repo installed`- install PHP using yum (*https://rpms.remirepo.net/enterprise/remi-release-7.rpm*)
11. `PHP is installed`- install packages: php80, php80-php, php80-php-mysqlnd, php80-php-pecl-mysql
12. `download wordpress && extract wp` - download and extracct WordPress from https://pl.wordpress.org/latest-pl_PL.tar.gz
13. `copy vhost cfg` - put vhost configuration file to the target place on server (*/etc/httpd/conf.d/blog.conf*)
14. `copy wp cfg` - put WordPress configuration file to the target place on server (*/var/www/wordpress/wp-config.php*)
15. `reload apache` - start apache
<br>

![The Start Page of WordPress](/files/images/wp.jpg "The Start Page of WordPress")

