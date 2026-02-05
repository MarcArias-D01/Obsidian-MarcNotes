---
tags:
  - nginx
  - linux
  - ubuntu
---
**Nginx** es un servidor web y proxy inverso de alto rendimiento. Se usa para:
- Servir páginas web estáticas muy rápido.
- Actuar como **proxy inverso** para aplicaciones (redirigir tráfico a otros puertos/servicios).
- Manejar **balanceo de carga**, **caché**, **SSL/TLS** y **autenticación**.
- Es ligero, eficiente y soporta miles de conexiones concurrentes con bajo consumo de recursos.

Para backends interactivos o con streaming:

```conf
server {
    listen 80;
    server_name n8n.d01.cloud;
    return 301 https://$host$request_uri;
} 

server {
    listen 443 ssl http2 ;
    server_name n8n.d01.cloud;

    ssl_certificate /etc/letsencrypt/live/n8n.d01.cloud/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/n8n.d01.cloud/privkey.pem;

    if ($scheme = http) { return 301 https://$server_name$request_uri; }
    http2_push_preload on;
    add_header Strict-Transport-Security "max-age=31536000";

    location / {
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade"; # para el webspcket
        proxy_set_header Host $http_host;
        #proxy_set_header Origin $scheme://$http_host;
        proxy_set_header Origin $scheme://$host:443;
        proxy_cache off;
        proxy_buffering off;
        proxy_set_header X-Forwarded-Host $host:$server_port;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;         proxy_pass_request_headers on;
        proxy_pass http://127.0.0.1:5678;
        # # proxy_pass http://###.###.###.###:####;
    }
}
```

Para backend de Api estaticas:
```conf
server {

    listen 80;

    server_name ia-decal.d01.cloud;

    return 301 https://$host$request_uri;

}

  

server {
    listen 443 ssl http2 ;
    server_name ia-decal.d01.cloud;

    ssl_certificate /etc/letsencrypt/live/ia-decal.d01.cloud/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/ia-decal.d01.cloud/privkey.pem;
    if ($scheme = http) { return 301 https://$server_name$request_uri; }
    http2_push_preload on;
    add_header Strict-Transport-Security "max-age=31536000";
  
    location / {
        proxy_pass http://127.0.0.1:7860/;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;


        auth_basic "Protected IA";
        auth_basic_user_file /etc/nginx/.htpasswd;
    }
}
```

## AUTH

EL último ejemplo tiene basic auth. Para crear la auth seguir los siguientes pasos:

- Instalar `htpasswd`
```bash
sudo apt-get install apache2-utils
```

- Crear el archivo y añadir usuario
```bash
sudo htpasswd -c /etc/nginx/.htpasswd usuario1
```
*⚠️ Solo usar `-c` la primera vez. Para añadir más usuarios, no uses `-c`, porque sobrescribe*

- Configurar nginx como en el ejemplo de api estática. Añadir estas lineas al final de location
```conf
auth_basic "Acceso restringido";
auth_basic_user_file /etc/nginx/.htpasswd;
```

- Comprobar antes de reiniciar que la configuración es la correcta
```bash
  sudo nginx -t
```

- Reiniciar nginx
```bash
sudo systemctl reload nginx
```