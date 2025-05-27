server {
    listen 80;
    server_name tsiul.ru www.tsiul.ru;
    server_tokens off;

    location /.well-known/acme-challenge/ {
        root /var/www/certbot;
    }

    location / {
        return 301 https://$host$request_uri;
    }
}

server {
    listen 443 ssl;
    server_name tsiul.ru;
    server_tokens off;

    ssl_certificate /etc/nginx/ssl/live/tsiul.ru/fullchain.pem;
    ssl_certificate_key /etc/nginx/ssl/live/tsiul.ru/privkey.pem;
    include /etc/nginx/ssl/options-ssl-nginx.conf;
    ssl_dhparam /etc/nginx/ssl/ssl-dhparams.pem;

    location / {
        proxy_pass http://app:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}