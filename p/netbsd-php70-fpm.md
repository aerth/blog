+++
date = "2016-02-12T16:16:02Z"
tags = ["php sucks", "nginx", "netbsd", "pkgsrc"]
title = "netbsd php70 fpm"

+++

# How to build php-fpm 7.0 on netbsd from pkgsrc

## And run it through nginx intertwined with another app.

# cat /mk.conf

```
PKG_OPTIONS.nginx+=     naxsi
PKG_RCD_SCRIPTS=YES
PHP_VERSIONS_ACCEPTED=70
```

# cat /usr/pkgsrc/meta-pkgs/php70-extensions/Makefile

```
# Comment out these lines:

#DEPENDS+=      php>=${PHP_VERSION}<${NEXT_VERS}:${PHPPKGSRCDIR}
#DEPENDS+=      ${APACHE_PKG_PREFIX}-${PHP_PKG_PREFIX}>=${PHP_VERSION}<${NEXT_VERS}:../../www/ap-php
```

$ cd /usr/pkgsrc/meta-pkgs/php70-extensions/
$ make clean && make update

$ cd /usr/pkgsrc/www/nginx
$ make clean && make update 

# cat /usr/pkg/etc/nginx/nginx.conf

```

user   nginx  nginx;
worker_processes  1;
#error_log  /var/log/nginx/error.log;                                                                                      $
error_log  /var/log/nginx/error.log  debug;
#error_log  /var/log/nginx/error.log  info;
#pid        /var/run/nginx.pid;
events {
    worker_connections  1024;
}
http {
        server_tokens off;
        # server_names_hash_bucket_size 64;
        server_name_in_redirect off;
    include /usr/pkg/etc/nginx/naxsi_core.rules;
    include       /usr/pkg/etc/nginx/mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    #tcp_nopush     on;
    #keepalive_timeout  0;
    keepalive_timeout  65;
    #gzip  on;
        include /usr/pkg/etc/nginx/conf.d/*.conf;
        include /usr/pkg/etc/nginx/sites-enabled/*;
}


```

# cat /usr/pkg/etc/nginx/sites-enabled/_default
# Personally, I dont like php running on / on the default IP
# Use this to route to a specific server running on 6099
server {

        server_name default_address;
        listen 80;
        location / {
        proxy_pass http://127.0.0.1:6099;
        }

}


# cat /usr/pkg/etc/nginx/sites-enabled/example.com

```
server {
        server_name isupon.us;
        error_page 404 /srv/live/_default/404.html;
        root   /srv/live/isupon.us/public;

# This shows our static page on :6099 for every request that isn't /
# This includes /index.php and /index.php?whatever
# Don't use those kind of URLs.

        location ~ $ {
        proxy_pass http://127.0.0.1:6099;
        }

        error_page 404             /404.html;
        error_page 500 502 503 504 /50x.html;

        location = / {
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root/index.php;
        fastcgi_param HTTPS off;
        include fastcgi_params;
        }

    # Generated thumbnail images
    location ~* /thumbs/(.*)$ {
        try_files $uri $uri/ /index.php?$query_string;
    }

    # Bolt backend access
    #
    # NOTE: If you set a custom branding path, you will need to change '/bolt/' 
    #       here to match
    location ~* /bolt/(.*)$ {
        try_files $uri $uri/ /index.php?$query_string;
    }

    # Backend async routes
    location ~* /async/(.*)$ {
        try_files $uri $uri/ /index.php?$query_string;
    }

    # Enforce caching for certain file extension types
    location ~* \.(?:ico|css|js|gif|jpe?g|png|ttf|woff|woff2)$ {
        access_log off;
        expires 30d;
        add_header Pragma public;
        add_header Cache-Control "public, mustrevalidate, proxy-revalidate";
    }

    # Don't create logs for favicon.ico or robots.txt requests
    location = /(?:favicon.ico|robots.txt) {
        access_log off;
        log_not_found off;
    }

    # Block PHP files from being run in upload (files), app, theme and extension directories
    location ~* /(?:app|extensions|files|theme)/(.*)\.php$ {
        deny all;
    }

    # Block hidden files
    location ~ /\. {
        deny all;
    }

    # Block access to Sqlite database files
    location ~ /\.(?:db)$ {
        deny all;
    }

    # Block access to the app, cache & vendor directories
    location ~ /(?:app|src|tests|vendor) {
        deny all;
    }

    # Block access to certain JSON files
    location ~ /(?:bower|composer|jsdoc|package)\.json$ {
        deny all;
    }

    # Block access to Markdown, Twig & YAML files directly
    location ~* /(.*)\.(?:dist|markdown|md|twig|yaml|yml)$ {
        deny all;
    }




}

```

# Now, requests to example.com show your php web app.

# Other requests go to your other app.

durr

