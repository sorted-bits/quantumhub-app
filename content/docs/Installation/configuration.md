---
title: Configuration
weight: 3
---

## Configuration file

```yaml
web:
  port: 3000 # The port the webserver listens to

instance_name: quantumhub

log:
  level: info
  included_modules:
    - example-device
  excluded_modules:
    - other-package

mqtt:
  host: <mqtt broker host> # The host of your MQTT broker
# port: 1883 # The port your MQTT broker is listening on
# username: # The username to authenticate with
# password: # The password to authenticate with
# protocol: mqtt # The protocol to use for MQTT, can be mqtt or ws
# validate_certificate: true # Whether to validate the certificate of the MQTT broker
  base_topic: qt # The base topic to use for MQTT

storage:
  file: 'storage.sqlite'
  dependencies: 'packages'

dependencies:
  - repository: https://github.com/sorted-bits/example-package
    file: example-device.yaml
  - example-climate
  - repository: /Volumes/Projects/quantumhub/modules/modbus-solarman
    file: growatt-mod-tl3-x.yaml

packages:
  - package: example-device
    identifier: new_york_clock
    name: New York Clock
    timezone: America/New_York
  - package: example-device
    identifier: amsterdam_clock
    name: Amsterdam Clock
    timezone: Europe/Amsterdam

homeassistant:
# availability: true # Whether to publish availability messages
# base_topic: homeassistant # The base topic to use for Home Assistant discovery

```

## web

```yaml
web:
  port: 3000 # The port the webserver listens to
```

#### `port`
The port the webserver listens to present the UI and API. *Default: `3000`*

## instance_name

```yaml
instance_name: quantumhub
```

This instance name is used in the topics that are published to the MQTT broker. Every instance of QuantumHub should have a unique name. *Default: `quantumhub`*

## log

```yaml
log:
  level: info
  included_modules:
   - example-device
  excluded_modules:
   - other-package  
```

#### `level`

The log level to use, when outputting to the console.

This can be one of the following:
- `TRACE`
- `DEBUG`
- `INFO`
- `WARN`
- `ERROR`
- `FATAL`

*Default: `INFO`*

#### `included_modules`

The modules to include in the log output. If a module is not included in the log output, it will not be outputted.

*Default: `[]`*

#### `excluded_modules`

The modules to exclude from the log output. If a module is excluded from the log output, it will not be outputted **even if it is included in the `included_modules` list**.

*Default: `[]`*

## mqtt

```yaml
mqtt:
  host: <mqtt broker host> # The host of your MQTT broker
# port: 1883 # The port your MQTT broker is listening on
# username: # The username to authenticate with
# password: # The password to authenticate with
# protocol: mqtt # The protocol to use for MQTT, can be mqtt or ws
# validate_certificate: true # Whether to validate the certificate of the MQTT broker
  base_topic: quantumhub # The base topic to use for MQTT
```

#### `host`
The host of your MQTT broker. *Default: `localhost`*

#### `port`
The port your MQTT broker is listening on. *Default: `1883`*

#### `username`
The username to authenticate with. *Default: `<empty>`*

#### `password`
The password to authenticate with. *Default: `<empty>`*

#### `protocol`
The protocol to use for MQTT, can be mqtt or ws. *Default: `mqtt`*

#### `validate_certificate`
Whether to validate the certificate of the MQTT broker. *Default: `true`*

#### `base_topic`
The base topic to use for MQTT. *Default: `quantumhub`*

## storage

```yaml
storage:
  file: 'storage.sqlite'
  dependencies: 'packages'
```

#### `file`
The file to use for sqlite storage. This file should only contain data that should be persisted between restarts. Deleting this file will cause the data to be reset. *Default: `storage.sqlite`*. 

#### `dependencies`
The path to the folder where the dependencies are installed to. *Default: `packages`*

## dependencies

```yaml
dependencies:
  - repository: https://github.com/sorted-bits/example-package
    file: example-device.yaml
  - example-climate
  - repository: /Volumes/Projects/quantumhub/modules/modbus-solarman
    file: growatt-mod-tl3-x.yaml
```

The `dependencies` section is used to specify the dependencies for the QuantumHub instance. There are 3 types of dependencies:

1. **Git repository**

```yaml
  - repository: https://github.com/sorted-bits/example-package
    file: example-device.yaml
```

When a repository is specified that does not start with `/`, it is assumed to be an online git repository. We will try to clone this repository to the `dependencies` folder using `git clone`.


2. **Dependency from name**

```yaml
  - example-climate
```

When a dependency is specified by it's name only, we will try to resolve this package using the [online package registry](https://quantumhub.app/packages.json).

3. **Local folder**

```yaml 
  - repository: /Volumes/Projects/quantumhub/modules/modbus-solarman
    file: growatt-mod-tl3-x.yaml
```

When a repository is specified that starts with `/`, it is assumed to be a local folder. We will use this folder as the dependency and no installation will be performed.

## packages

```yaml
packages:
  - package: example-device
    identifier: new_york_clock
    name: New York Clock
    timezone: America/New_York
```      

##### `package`
This should be the name of the package to use for this device.

##### `identifier`
The identifier for the device, this should be unique in your QuantumHub instance.

##### `name`
The name of the device. Used for display purposes.

##### `config_file`
**IF** your package is not in the `packages` folder, you can specify the path to the config file here.

##### `timezone`
If a package can have a specific configuration, it should be listed here (e.g. `timezone` for the `example-device`). So `timezone` is just an example and not needed for all packages.

## homeassistant

```yaml
homeassistant:
  availability: true # Whether to publish availability messages
  base_topic: homeassistant # The base topic to use for Home Assistant discovery
```

#### `availability`
Whether to publish availability messages. *Default: `true`*

#### `base_topic`
The base topic to use for Home Assistant discovery. This usually should not be changed as it is the default for the Home Assistant MQTT integration. *Default: `homeassistant`*

