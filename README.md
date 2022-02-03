## Virtual Hosting using nginx
```
nano /etc/nginx/conf.d/crud.conf
```
```
server {
        listen 80;
        server_name crud;
	#expires 1d;

	location / {

          #proxy_cache my_cache;
	  #proxy_buffering        on;
	  #proxy_cache_valid      200  1d;
	  #proxy_cache_use_stale  error timeout invalid_header updating
          #http_500 http_502 http_503 http_504;

          proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
          proxy_set_header X-Forwarded-Proto $scheme;
          proxy_set_header X-Real-IP $remote_addr;
	  proxy_set_header Host $host;
          proxy_pass  http://127.0.0.1:8080;
        }
}
```

## NGINX STATUS & RESTART
```
sudo systemctl status nginx
sudo systemctl reload nginx
sudo systemctl restart nginx
```

## Systemd service file
```
sudo nano /lib/systemd/system/crud.service
```

```
[Unit]
Description=Spedfit website
After=network.target

[Service]
Type=simple
Restart=always
RestartSec=5s
WorkingDirectory=/home/raihan/go/src/golang_crud/
ExecStart=/home/raihan/go/src/golang_crud/golang_crud

[Install]
WantedBy=multi-user.target
```

## Set permission
```
sudo chmod 664 /lib/systemd/system/crud.service

```

## Reload systemd daemon
```
sudo systemctl daemon-reload
```
## Check service status & Restart 
```
sudo service crud status
sudo service crud start
```

## Enable to start services automatically at boot
```
sudo systemctl enable crud
```

```
cd /etc/nginx/sites-available
```
```
server {
    server_name crud www.crud;

    location / {
        proxy_pass http://localhost:8080;
    }
}
```