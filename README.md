nodebb-setup
============

repo
redis-server
nodejs
nodebb
nginx
 
sudo nano /etc/nginx/sites-available/costco

server {
     listen 80;
     server_name costco.bbnode.info;
    
     location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-NginX-Proxy true;

        proxy_pass      http://127.0.0.1:4567/;
        proxy_redirect off;

        # Sockect.IO Support
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}

sudo ln -s /etc/nginx/sites-available/costco

sudo /etc/init.d/nginx restart
