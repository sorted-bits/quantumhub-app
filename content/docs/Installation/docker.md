---
title: Docker
type: docs
weight: 1
---

### Dockerhub

QuantumHub is available on Dockerhub as [sortedbit/quantumhub](https://hub.docker.com/repository/docker/sortedbit/quantumhub/general).

### Docker Compose

```yaml
---
version: "2.1"
services:
  sabnzbd:
    image: sortedbit/quantumhub:latest
    container_name: quantumhub
    environment:
      - TZ=Etc/UTC
    ports:
      - 3000:3000
    volumes:
      - /your/config/file.yaml:/home/node/app/config.yaml
      - /your/packages/folder:/home/node/packages
    restart: always
```

#### Volumes

##### Configuration file
**Path:** `/home/node/app/config.yaml`  

This is the configuration file for QuantumHub. A default configuration file is provided, but adding this as a volume allows you to override the default configuration.

##### Packages folder
**Path:** `/home/node/packages`  

This is the folder containing the packages you want to use. There is also a way to specify a custom path in the configuration file, see [Configuration](/docs/installation/configuration/). You can either use the included `/home/node/packages` or specify a custom path. The default path includes an `example-package`.
