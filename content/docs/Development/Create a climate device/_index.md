---
title: Create a climate device
type: docs
weight: 3
---

# Create a climate device

{{< hint danger >}}
**Work in progress**  
This example is not complete and is still a work in progress. During the development of QuantumHub it became clear that the climate device is a very complex device, with a lot of features. The example below is the minimal working example.
{{< /hint >}}

The `test-device` repository contains an example climate device, which can be used as a starting point for creating your own climate device. It uses some basic attributes, which I will explain here.

## Configuration

As explained in `this file` your device needs a YAML file which defines the package and the attributes a device has available.

The following configuration is used in the example climate device:

```yaml
package:
  name: example-climate
  version: 1.0.0
  description: QuantumHub module for testing the integration
  author: Wim Haanstra
  entry: example-climate/example-climate.ts

attributes:
  heater:
    name: Heater
    type: climate
    optimistic: true
    has_fanmode: false
    has_swingmode: false
    has_presetmode: false
    has_humidity_control: false
```

## Climate Features

The configuration of a `climate` attributes has a couple of options, which define how QuantumHub will register the device in Home Assistant.

### `has_fanmode`
Does the device have fanmodes? If it does, you would also need to set the `fan_modes` attribute with possible fanmodes.

### `has_swingmode`
### `has_presetmode`
### `has_humidity_control`


