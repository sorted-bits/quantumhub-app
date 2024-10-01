---
title: Package
type: docs
weight: 1
---

### Package.json

Because QuantumHub requires your device to follow certain interfaces, we probably want to use a package.json file to define the dependencies. The dependency that is required is `quantumhub-sdk`.

```json
{
  "name": "internal-test",
  "version": "1.0.0",
  "description": "",
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "quantumhub-sdk": "<version>"
  }
}
```

### Configuration

Your device should have a configuration file, which is used to configure the device. This configuration file is used to pass the configuration to the device.

```yaml
package:
  name: example-sensor
  version: 1.0.0
  description: <Your description of your device>
  author: <Your name>
  entry: example-sensor.ts

attributes:
  temperature:
    name: Temperature
    type: sensor
    unit_of_measurement: °C
    device_class: temperature
    state_class: measurement
```

#### Package configuration

```yaml
package:
  name: example-sensor
  version: 1.0.0
  description: <Your description of your device>
  author: <Your name>
  entry: example-sensor.ts
```

##### `name`

The `name` attribute is used to identify your device. It should be unique within your QuantumHub instance. This is the identifier that is used to instantiate the device.

##### `version`

The `version` of your device. This is displayed in the UI so the user can see if they are running the latest version.

##### `description`

The `description` attribute is used to describe your device. This is used to describe the device to the user.

##### `author`

The `author` attribute is used to identify the author of the device. This is used to identify the author of the device.

##### `entry`

The `entry` attribute is used to identify the entry file of the device. This is the file that is used to instantiate the device.

#### Device Attributes

```yaml
attributes:
  temperature:
    name: Temperature
    type: sensor
    unit_of_measurement: °C
    device_class: temperature
    state_class: measurement    
```


{{< callout type="warning" >}}
The key used for each attribute should be unique within your configuration file.
{{< /callout >}}

For the description of the attributes, please refer to the [Attributes](/docs/development/sdk/device-attributes) page.
### Example

For an example on how to create a simple sensor, check out the [Create a simple sensor](/docs/development/create-a-simple-sensor) example.