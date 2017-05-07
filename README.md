# Docker 3proxy slim container
3proxy docker container based on alpine

## Build & run
Configure `docker-compose.yml` before
```
docker-compose up --build 3proxy
```

## Install as service (systemd)

Clone repository to `/opt/docker-3proxy` 

Create `/etc/systemd/system/3proxy.service`
```
[Unit]
Description=3proxy Service  
After=docker.service  
Requires=docker.service

[Service]
ExecStart=/usr/local/bin/docker-compose -f /opt/docker-3proxy/docker-compose.yml up --build
ExecStop=/usr/local/bin/docker-compose -f /opt/docker-3proxy/docker-compose.yml stop

[Install]
WantedBy=multi-user.target  
```

Install service
```
systemctl enable 3proxy.service
```