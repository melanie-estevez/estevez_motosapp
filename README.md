# estevez_motosappreact
## Autor: Melanie Estevez
npm run build
sudo rm -rf /var/www/estevez_motosapp/*
sudo cp -r build/* /var/www/estevez_motosapp/

server {
    listen 80;
    server_name http://estevez-rider.uaeftt-ute.site;

    root /var/www/react-app;
    index index.html;

    # Seguridad básica
    add_header X-Content-Type-Options nosniff;
    add_header X-Frame-Options SAMEORIGIN;
    add_header Referrer-Policy strict-origin-when-cross-origin;

    location / {
        try_files $uri $uri/ /index.html;
    }

    # Cache de assets (ajusta si lo deseas)
    location ~* \.(js|css|png|jpg|jpeg|gif|svg|ico|woff2?)$ {
        expires 7d;
        add_header Cache-Control "public, max-age=604800, immutable";
        try_files $uri =404;
    }
}

sudo ln -s /etc/nginx/sites-available/estevez_motosapp /etc/nginx/sites-enabled/estevez_motosapp
sudo nginx -t
sudo systemctl reload nginx

sudo nano /etc/nginx/sites-available/estevez_motosapp