---
title: QuantumHub
type: default
---

### Purpose

The purpose of `QuantumHub` is to be able to easily develop support for hardware using the Home Assistant MQTT integration. By using NodeJS and simple examples, I try to make developing for Home Assistant more accessible.

This also makes sure that your code does not need to be merged into the Home Assistant repository, but can live in its own repository.

### Features

- Easy configuration via YAML
- Web interface to check your devices and their states
- SDK to easily develop your own integrations

### Current limitations

- Manual configuration of units, etc.
- We are running a TypeScript version in our Docker
- Not all device types are supported yet, please check the [DeviceType](https://github.com/sorted-bits/quantumhub-sdk/blob/main/src/enums/device-type.ts) enum for more information.

### Jump in

{{< cards cols="1" >}}
  {{< card link="/docs/installation" title="Installation" >}}
  {{< card link="/docs/development" title="Development" >}}
  {{< card link="/docs/sdk" title="SDK" >}}
{{< /cards >}}
