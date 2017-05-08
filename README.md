# Docker 3proxy slim container
3proxy docker container based on alpine

## Build & run
Configure `docker-compose.yml` before
```
docker-compose up --build 3proxy
```

## Install as service (systemd)

Install `docker`, `docker-compose`, `git`

Clone repository
```
mkdir /opt && cd /opt
git clone https://github.com/avin/3proxy-docker-slim.git
``` 

Create `/etc/systemd/system/3proxy-docker.service`
```
[Unit]
Description=3proxy Service  
After=docker.service  
Requires=docker.service

[Service]
ExecStart=/usr/local/bin/docker-compose -f /opt/3proxy-docker-slim/docker-compose.yml up --build
ExecStop=/usr/local/bin/docker-compose -f /opt/3proxy-docker-slim/docker-compose.yml stop -t 2

[Install]
WantedBy=multi-user.target  
```

Install service
```
systemctl enable 3proxy-docker.service
```

Enjoy!