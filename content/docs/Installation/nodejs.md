---
title: Node.js
type: docs
weight: 2
---

{{< callout type="warning" >}}
  This is currently a work in progress and using QuantumHub like this is only recommended when developing your own packages.
{{< /callout >}}

### Prerequisites

- Install [Node.js](https://nodejs.org/en/download/).
- Install [Git](https://git-scm.com/downloads).
- Configure the [Home Assistant MQTT integration](https://www.home-assistant.io/integrations/mqtt/).

{{% steps %}}

### Clone the repository

```bash
git clone https://github.com/sorted-bits/quantumhub.git
```

### Install dependencies

```bash
cd quantumhub
npm install
```

### Configure the server

```bash
cp config.yaml.example config.yaml
```

Edit the configuration file to your liking.

### Start the server

```bash
npm start
```

{{% /steps %}}

