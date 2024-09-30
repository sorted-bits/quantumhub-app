---
title: Device
type: docs
weight: 1
---

# Device

## Required methods

### `init(provider: Provider): Promise<boolean>;`  
Called after the package is loaded from disk and the provider for your device is initialized. This Provider gives you access to all the exposed features of QuantumHub, so you'll probably want to store it in your device class. 

You can return false if something goes wrong, in that case the device will be disabled in the UI and there will be no attempt to start your device.

### `start(): Promise<void>;`  
Called when the device is being started, during startup this is immediately after the init method (if the device isn't disabled in the config, and init passed succesfully). 

This is method returns a promise, but QuantumHub will not wait for it to finish, it will continue starting other devices. 

### `stop(): Promise<void>;`  
Called when the device is being stopped. This is only called when the device is stopped using the stop button in the QuantumHub UI or when QuantumHub is shutting down.

### `destroy(): Promise<void>;`  
Called when the device is being destroyed. This is only called when QuantumHub is shutting down.

### `valueChanged(attribute: Attribute, value: any): Promise<void>;`  
 Called when the value of an attribute is changed, for example a value is changed by the Home Assistant MQTT integration.


## Optional methods

### `onMessage?(topic: string, message: Buffer): Promise<void>;`

When your device is manually subscribed to a topic on the MQTT broker, this method is called when a new value is received on that topic.

Check out [`provider.mqtt.subscribeToTopic`](/docs/development/sdk/provider/#subscribetotopictopic-string-promisevoid) for more information.

### `onSceneTriggered?(attribute: SceneAttribute): Promise<void>;`

When your device exposes a scene to Home Assistant, this method is called when the scene is triggered. The supplied parameter contains the `SceneAttribute` connected. Check out [`SceneAttribute`](/docs/development/sdk/device-attributes/#sceneattribute) for more information.

## Github

[device.ts](https://github.com/sorted-bits/quantumhub-sdk/blob/main/src/interfaces/device.ts).

