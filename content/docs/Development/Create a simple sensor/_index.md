---
title: Create a simple sensor
type: docs
weight: 2
---

**Really basic example**  
This example is really basic and only shows the absolute basics of how to create a simple sensor.

## Prerequisites

- Install [Node.js](https://nodejs.org/en/download/)
- Prepare a folder where you are going to create your device, e.g. `example-sensor`
  - Open a terminal in that folder.
  - Run `npm init -y` to create a `package.json` file.
  - Run `npm install quantumhub-sdk` to install the QuantumHub SDK.
  - Open the folder in your favorite IDE, I am using [Cursor](https://cursor.sh/).

## Create a configuration file
Every device needs a configuration file, which defines the package and the attributes a device has available. In this example we will create a simple temperature sensor. Check out the [configuration reference](../reference/configuration) for more information.

Create a file called `example-sensor.yaml` and add the following content:
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

In the configuration file we define a value for `entry`, this needs to be a relative path to the file where your device is implemented.

## Create the device file

Create a file called `example-sensor.ts` in the location you defined in the configuration file and add the following content:

```typescript
import { Device, Provider } from 'quantumhub-sdk';

class ExampleSensor implements Device {
  private provider!: Provider;
  private timeoutId: undefined | NodeJS.Timeout;

  /**
   * This method is called when the packages are being loaded from disk and being cached by the QuantumHub server.
   * You will receive the Provider instance, which you can store in the class for later use.
   *
   * @param provider
   * @returns
   */
  init = async (provider: Provider): Promise<boolean> => {
    this.provider = provider;

    return true;
  };

  /**
   * This method is called when the device is being started. This is always 
   * AFTER the init method and only when init returned true.
   */
  start = async (): Promise<void> => {
    this.timeoutId = this.provider.timeout.set(async () => {
      this.update();
    }, 5000);
  } 

  /**
   * This method is called when the device is being stopped. For example when the server is being stopped or the device
   * is manually stopped from the web interface.
   */
  stop = async (): Promise<void> => {
    if (this.timeoutId) {
      this.provider.timeout.clear(this.timeoutId);
      this.timeoutId = undefined;
    }    
  }

  /**
   * This method is called when the device is being destroyed. 
   * This is always the last method that is called on the device.
   */
  destroy = async (): Promise<void> => {
  }

  /**
   * A simple method that uses a timeout to loop indefinitely and update the temperature attribute.
   */
  private update = async (): Promise<void> => {
    // In our example we are updating the temperature every 5 seconds with a random value.
    const randomValue = Math.floor(Math.random() * 100);

    // Here we are triggering the QuantumHub API to update the value of the `temperature` attribute.
    this.provider.setAttributeValue('temperature', randomValue.toString());

    // We are calling the update method again in 5 seconds.
    this.timeoutId = this.provider.timeout.set(this.update.bind(this), 5000);
  }
}

export default ExampleSensor;
```

## Updating the QuantumHub configuration

Make sure you copy the `example-sensor` folder to the `packages` folder of QuantumHub.

During the [installation of QuantumHub](/install), you created a [configuration file](/docs/Development/Configuration). Open the file and add your device to the `packages` section.

```yaml
packages:
  root: ./packages
  configuration:
    - package: example-sensor
      identifier: random-sensor
      name: My first random sensor
```

## Restart

Restart the QuantumHub server.