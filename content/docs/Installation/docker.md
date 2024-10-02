---
title: Docker
type: docs
weight: 1
---
{{< tabs items="Easy,Advanced" >}}

{{< tab >}}
### Prerequisites

- Install <i class="fa-brands fa-docker"></i> [Docker](https://docs.docker.com/get-docker/)
- Install [Docker Compose](https://docs.docker.com/compose/install/)

{{% steps %}}

### Create the docker-compose.yml file

```yaml
---
version: "2.1"
services:
  quantumhub:
    image: sortedbit/quantumhub:latest
    container_name: quantumhub
    environment:
      - TZ=Etc/UTC
    ports:
      - 3000:3000
    volumes:
      - ./config.yaml:/home/node/app/config.yaml
    restart: always
```

### Grab the example configuration file

```bash
wget https://raw.githubusercontent.com/sorted-bits/quantumhub/main/config.yaml.example -O config.yaml
```

### Update the configuration file

Edit the configuration file so it matches your setup.

### Run the container

```bash
docker compose up
```

### Access the Webinterface

Open your browser and navigate to [http://localhost:3000](http://localhost:3000).

{{% /steps %}}
{{< /tab >}}

{{< tab >}}
### Dockerhub

QuantumHub is available on Dockerhub as [sortedbit/quantumhub](https://hub.docker.com/repository/docker/sortedbit/quantumhub/general).

### Docker Compose

```yaml
---
version: "2.1"
services:
  quantumhub:
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

This is the configuration file for QuantumHub. An example configuration can be found [here](https://github.com/sorted-bits/quantumhub/blob/main/config.yaml.example).

##### Packages folder
**Path:** `/home/node/packages`  

This is the folder containing the packages you want to use. There is also a way to specify a custom path in the configuration file, see [Configuration](/docs/installation/configuration/). You can either use the included `/home/node/packages` or specify a custom path. The default path includes an `example-package`.

#### Ports

**3000:** The port the webserver listens to, this exposes the QuantumHub API and the QuantumHub Webinterface.

{{< /tab >}}


{{< /tabs >}}
