# Aria2, with integrated Aria2-NG Frontends

[![Docker Build Status](https://img.shields.io/docker/build/zyao89/aria2-with-webui.svg)](https://hub.docker.com/r/zyao89/aria2-with-webui) [![Docker Automated build](https://img.shields.io/docker/automated/zyao89/aria2-with-webui.svg)](https://hub.docker.com/r/zyao89/aria2-with-webui) [![Docker Stars](https://img.shields.io/docker/stars/zyao89/aria2-with-webui.svg)](https://hub.docker.com/r/zyao89/aria2-with-webui) [![Docker Pulls](https://img.shields.io/docker/pulls/zyao89/aria2-with-webui.svg)](https://hub.docker.com/r/zyao89/aria2-with-webui)

This Dockerfile build an image for [aria2](https://github.com/aria2/aria2) with [AriaNg](https://github.com/mayswind/AriaNg) frontends.

## Quick Start

```shell
docker run -d --name aria2-webui \
-p 80:80 -p 6800:6800 \
zyao89/aria2-with-webui
```

## Advanced

```shell
docker run -d --name aria2-webui \
-p 80:80 -p 6800:6800 \
-e PGID=1000 \
-e PUID=1000 \
-e SECRET=your_password \
-e SECURE=true \
-e CERTIFICATE=/server/path/to/your_cert \
-e PRIVATEKEY=/server/path/to/your_key \
-e LOGPATH=/logs.log \
-v /path/to/persist/data:/data \
zyao89/aria2-with-webui
```

Which will make the Aria2 client accessible over HTTP from port 6800, with the WebUI being accessible from 80. If you define SECRET, this token can be used to communicate with the Aria2 daemon. Define SECURE as true and pass the cert and private key, to enable aria2 RPC transport encrypted by SSL/TLS.

If you want to use your aria2 configuration file, you need to mount the /conf folder to a volume.

## Docker Compose

```yaml
version: "3"

services:
  aria2:
    container_name: aria2
    image: zyao89/aria2-with-webui
    restart: always
    ports:
      - "6800:6800"
      - "80:80"
    environment:
      - PGID=${PGID:-1000}
      - PUID=${PUID:-1000}
      - SECRET=your_password
      - SEEDRATIO=2
      - SEEDTIME=0
      - SECURE=true
      - CERTIFICATE=/server/path/to/your_cert
      - PRIVATEKEY=/server/path/to/your_key
      - LOGPATH=/logs.log
    volumes:
      - /path/to/persist/data:/data
```

## Thanks

This docker image is based on [onisuly](https://hub.docker.com/r/onisuly/aria2-with-webui/)'s docker image.
