# Nginx web server for Ubuntu

## Installation

```
$ sudo apt-get update
$ sudo apt install nginx
$ sudo ufw app list
$ sudo ufw enable
$ sudo ufw allow 'Nginx HTTP'
$ sudo ufw status
$ systemctl status nginx
$ curl -4 icanhazip.com
```

To verify the Nginx installation, visit `http://server_ip_address` on your browser.

## Managing Nginx
```
$ systemctl stop nginx
$ systemctl start nginx
$ systemctl restart nginx
$ systemctl reload nginx
$ systemctl disable nginx
$ systemctl enable nginx
```

## Modifying default Index file

```
$ gedit /var/www/html/index.nginx-debian.html
$ sudo systemctl restart nginx
$ curl -4 icanhazip.com
```
> Visit `http://server_ip_address` on your browser.
