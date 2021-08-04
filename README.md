# shopifyappcmd

# install domain host in nginx


Create Virtual Host in Nginx :


1. sudo mkdir -p /var/www/example.com/public_html

2. sudo chown -R $USER:$USER /var/www/example.com/public_html

3. sudo chmod -R 755 /var/www

4. sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/example.com

5. sudo nano /etc/nginx/sites-available/example.com

Clear file and paste this code in file, replace example.com to your hostname

    server {
        listen 80;
        listen [::]:80;
        server_name example.com;
        root /var/www/example.com/public_html;
        index index.php index.html index.htm;
        location / {
                 try_files $uri $uri/ /index.php?$args;
        }
        location ~ \.php$ {
            try_files $uri =404;
            include /etc/nginx/fastcgi_params;
            fastcgi_pass unix:/run/php/php7.3-fpm.sock; 
            fastcgi_index index.php;
            fastcgi_param SCRIPT_FILENAME /var/www/example.com/public_html/$fastcgi_script_name;
        }
    }


6. sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/

7. sudo nginx -t

8. sudo systemctl restart nginx

9. sudo nano /etc/hosts

add your domain:
#For localhost:
127.0.0.0.1   <example.com>

#For live:
<serverIP>   <example.com>

