# Serving a Static Website Using NGINX

A complete guide to deploying a static website with **NGINX on Ubuntu**, featuring custom error pages and virtual host configuration.

---

##  Project Repository
**Live Demo:** [143.110.171.150](http://143.110.171.150)

---

##  Prerequisites
- Ubuntu 20.04/22.04 LTS
- sudo privileges
- Domain name (optional)
- Basic terminal skills

---

##  Quick Start

### 1. Install NGINX
```bash
sudo apt update && sudo apt install nginx -y
```

### 2. Clone and Place Static Files
```bash
git clone https://github.com/jaiswaladi246/static-site.git
cd static-site
sudo mkdir -p /var/www/static-site
sudo cp -r * /var/www/static-site/
```

## 3. Set correct ownership for the NGINX user:

```bash
sudo chown -R www-data:www-data /var/www/static-site
```

## 4. Configure NGINX Virtual Host
```bash
sudo vi /etc/nginx/sites-available/static-site
```
```bash
server {
    listen 80;
    server_name xxx.xxx.xxx.xxx;

    root /var/www/static-site;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    error_page 404 /404.html;
    error_page 500 502 503 504 /500.html;

    location = /404.html {
        root /var/www/static-site;
        internal;
    }

    location = /500.html {
        root /var/www/static-site;
        internal;
    }
}

```

### Enable the site and reload NGINX:

``` bash
sudo ln -s /etc/nginx/sites-available/static-site /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

---

This `README.md` includes all the steps for setting up NGINX, deploying a static website, and configuring custom 404/500 error pages, along with HTML for the error pages and other essential details. 

Let me know if you need further adjustments!

