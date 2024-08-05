## Webserver Configuration

Easily deploy the latest version of Skyport Panel on your own domain by following these steps:

## Dependencies

* Nginx
* SSL ( optional )

### Example Dependency Installation

The commands below are simply an example of how you might install these dependencies on Ubuntu 24.04. Please consult with your
operating system's package manager to determine the correct packages to install.

```sh
sudo apt update
sudo apt install -y nginx
```

## Installation: using Nginx

First, remove the default NGINX configuration.

```bash
rm /etc/nginx/sites-enabled/default
```

Now, you should paste the contents of the file below, replacing `<domain>` with your domain name and `<port>` for the current active port inside of a file called `skyport.conf` and place the file in `/etc/nginx/sites-available/`

### With SSL ( Secure Sockets Layer )

```nginx
server {
    listen 80;
    server_name <domain>;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name <domain>;

    access_log /var/log/nginx/panel-access.log;
    error_log /var/log/nginx/panel-error.log error;

    # SSL Configuration
    ssl_certificate /etc/letsencrypt/live/<domain>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<domain>/privkey.pem;
    ssl_session_cache shared:SSL:10m;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers "ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384";
    ssl_prefer_server_ciphers on;

    # Security Headers
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Robots-Tag none;
    add_header Content-Security-Policy "frame-ancestors 'self'";
    add_header X-Frame-Options DENY;
    add_header Referrer-Policy same-origin;

    location / {
        proxy_pass http://localhost:<port>;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    location ~ /\.ht {
        deny all;
    }
}

```

### Without SSL ( Secure Sockets Layer )

```nginx
server {
    listen 80;
    server_name <domain>;

    access_log /var/log/nginx/panel-access.log;
    error_log /var/log/nginx/panel-error.log error;

    # Security Headers
    add_header X-Content-Type-Options nosniff;
    add_header X-XSS-Protection "1; mode=block";
    add_header X-Robots-Tag none;
    add_header Content-Security-Policy "frame-ancestors 'self'";
    add_header X-Frame-Options DENY;
    add_header Referrer-Policy same-origin;

    location / {
        proxy_pass http://localhost:<port>;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }

    location ~ /\.ht {
        deny all;
    }
}

```

### Enabling Configuration  

The final step is to enable your Nginx configuration and restart it.

```bash
sudo ln -s /etc/nginx/sites-available/skyport.conf /etc/nginx/sites-enabled/
sudo systemctl restart nginx
```

# Done! Go to your Domain and view the new fresh update with no ip+port url :)
