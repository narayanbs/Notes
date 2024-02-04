#### Install Nginx

```bash
$ sudo apt update
$ sudo apt install nginx

$ sudo ufw status  

# if status is inactive then
$ sudo ufw enable

sudo ufw app list
```

**Output**
```bash
Available applications:
  Nginx Full
  Nginx HTTP
  Nginx HTTPS
```

  
```bash
sudo ufw allow 'Nginx HTTP'
sudo ufw status
```

**Output**
```bash
Status: active
To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere                  
Nginx HTTP                 ALLOW       Anywhere                  
OpenSSH (v6)               ALLOW       Anywhere (v6)             
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```

##### check web server status

```bash
systemctl status nginx
```

**Output**
```bash
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: en
   Active: active (running) since Fri 2021-10-01 21:36:15 UTC; 35s ago
     Docs: man:nginx(8)
 Main PID: 9039 (nginx)
    Tasks: 2 (limit: 1151)
   CGroup: /system.slice/nginx.service
           ├─9039 nginx: master process /usr/sbin/nginx -g daemon on; master_pro
           └─9041 nginx: worker process
           
`Notice (running)`
```

open browser and enter http://127.0.0.1 and you should get the nginx welcome page.
#### Managing Nginx

**To stop the web server:** `sudo systemctl stop nginx`
**To start the web server:** `sudo systemctl start nginx`
**To stop and start :** `sudo systemctl restart nginx`

If you are simply making configuration changes, you can often reload Nginx without dropping connections instead of restarting it. To do this, type the following:

`sudo systemctl reload nginx`

By default, Nginx is configured to start automatically when the server boots. If this is not what you want, you can disable this behaviour by typing the following:

`sudo systemctl disable nginx`

To re-enable the service to start up at boot, you can type the following:

`sudo systemctl enable nginx`

#### Setting up Server Blocks

Server blocks (similar to virtual hosts in Apache), can be used to encapsulate configuration details and host more than one domain from a 
single server. We will set up a domain called example.com and test.com

Create the directory for your_domain as follows, using the -p flag to create any necessary parent directories:
```bash
sudo mkdir -p /usr/share/nginx/example.com/html
sudo mkdir -p /usr/share/nginx/test.com/html
```

Next, assign ownership of the directory with the $USER environment variable:
```bash
sudo chown -R $USER:$USER /usr/share/nginx/example.com/html/
sudo chown -R $USER:$USER /usr/share/nginx/test.com/html/
```


The permissions of your web roots should be correct if you haven’t modified your umask value, but you can make sure by typing the following: `sudo chmod -R 775 /usr/share/nginx`

Next, create a sample index.html page using nano or your favorite editor:
`sudo nano /usr/share/nginx/example.com/html/index.html`
```html

<html>
    <head>
        <title>Welcome to Example.com!</title>
    </head>
    <body>
        <h1>Success! The example.com server block is working!</h1>
    </body>
</html>
```


`cp /usr/share/nginx/example.com/html/index.html /usr/share/nginx/test.com/html/`
change example.com to test.com

Create server block files for each domain.
By default, nginx contains one “default” server block inside of its main configuration file, nginx.conf. /etc/nginx/nginx.conf 
that looks like this
```bash

server {
        listen       80 default_server;
        listen       [::]:80 default_server;
        server_name  _;
        root         /usr/share/nginx/html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        location / {
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }
    }
…
```

Now Use this as a template for our conf.

`sudo nano /etc/nginx/conf.d/example.com.conf`

Firstly after that, you should review the listen directives. Only one of your server blocks on the server can have the default_server option enabled. This specifies which block should serve a request if the server_name requested does not match any of the available server blocks. This shouldn’t happen very frequently in real world scenarios since visitors will be accessing your site through your domain name.

You can choose to designate one of your sites as the “default” by including the default_server option in the listen directive, or you can leave the default server block enabled in nginx.conf, which will serve the content of the /usr/share/nginx/html directory if the requested host cannot be found.

In this guide, you’ll leave the “default” server block in place to serve non-matching requests, so your new example.com configuration will not contain default_server:

/etc/nginx/conf.d/example.com.conf
server {
        listen 80;
        listen [::]:80;

        . . .
}

Next, you need to modify the server_name to match requests for your first domain. You can additionally add any aliases that you need to match. In this tutorial, you will add an example.com and an www.example.com alias to demonstrate.
When we are finished our final file will be like this. 
```bash

server {
        listen 80;
        listen [::]:80;

        root /usr/share/nginx/example.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name example.com www.example.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

 
Use this as the basis for our second file
```bash
sudo cp /etc/nginx/conf.d/example.com.conf /etc/nginx/conf.d/test.com.conf

sudo nano /etc/nginx/conf.d/test.com.conf
```
```
server {
        listen 80;
        listen [::]:80;

		root /usr/share/nginx/test.com/html;
        index index.html index.htm index.nginx-debian.html;

        server_name test.com www.test.com;

        location / {
                try_files $uri $uri/ =404;
        }
}
```

Enable the server blocks by restarting nginx


```bash
sudo nginx -t
sudo systemctl restart nginx
```


modify /etc/hosts -- `sudo nano /etc/hosts`

127.0.0.1   localhost
. . .

127.0.0.1 example.com www.example.com
127.0.0.1 test.com www.test.com

Now test our results

http://example.com or http://test.com

Success! The example.com server block is working!
Success! The test.com server block is working!

