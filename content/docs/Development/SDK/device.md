---
title: Device
type: docs
weight: 1
---

# Device

## Required methods

### `init(provider: Provider): Promise<boolean>;`  
Called after the package is loaded from disk and the [`Provider`](/docs/development/sdk/provider/) for your device is initialized. This [`Provider`](/docs/development/sdk/provider/) gives you access to all the exposed features of QuantumHub, so you'll probably want to store it in your device class. 

You can return false if something goes wrong, in that case the device will be disabled in the UI and there will be no attempt to start your device.

### `start(): Promise<void>;`  
Called when the device is being started, during startup this is immediately after the init method (if the device isn't disabled in the config, and init passed succesfully). 

This is method returns a promise, but QuantumHub will not wait for it to finish, it will continue starting other devices. 

### `stop(): Promise<void>;`  
Called when the device is being stopped. This is only called when the device is stopped using the stop button in the QuantumHub UI or when QuantumHub is shutting down.

### `destroy(): Promise<void>;`  
Called when the device is being destroyed. This is only called when QuantumHub is shutting down.

### `valueChanged(attribute: Attribute, value: any): Promise<void>;`  
 Called when the value of an [`Attribute`](/docs/development/sdk/device-attributes/) is changed, for example a value is changed by the Home Assistant MQTT integration.


## Optional methods

## MQTT

### `onMessage?(topic: string, message: Buffer): Promise<void>;`

When your device is manually subscribed to a topic on the MQTT broker, this method is called when a new value is received on that topic.

Check out [`provider.mqtt.subscribeToTopic`](/docs/development/sdk/provider/#subscribetotopictopic-string-promisevoid) for more information.

## Scene

### `onSceneTriggered?(attribute: SceneAttribute): Promise<void>;`

When your device exposes a scene to Home Assistant, this method is called when the scene is triggered. The supplied parameter contains the triggered [`SceneAttribute`](/docs/development/sdk/device-attributes/#sceneattribute).

## Button

### `onButtonPressed?(attribute: ButtonAttribute): Promise<void>;`

When your device exposes a button to Home Assistant, this method is called when the button is pressed. The supplied parameter contains the triggered [`ButtonAttribute`](/docs/development/sdk/device-attributes/#buttonattribute).

## Select

### `onSelectChanged?(attribute: SelectAttribute, value: string): Promise<void>;`

When the value of a select attribute is changed, this method is called. The supplied parameter contains the changed [`SelectAttribute`](/docs/development/sdk/device-attributes/#selectattribute) and the selected value, which is supplied in the `options` field of the attribute.

## Number

### `onNumberChanged?(attribute: NumberAttribute, value: number): Promise<void>;`

When the value of a number attribute is changed, this method is called. The supplied parameter contains the changed [`NumberAttribute`](/docs/development/sdk/device-attributes/#numberattribute) and the new value.

## Switch

### `onSwitchChanged?(attribute: SwitchAttribute, value: boolean): Promise<void>;`

When the value of a switch attribute is changed, this method is called. The supplied parameter contains the changed [`SwitchAttribute`](/docs/development/sdk/device-attributes/#switchattribute) and the new value.

## Climate

### `onHvacModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;`

When the hvac mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/development/sdk/device-attributes/#climateattribute) and the new value.

### `onClimateModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;`

When the climate mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/development/sdk/device-attributes/#climateattribute) and the new value.

### `onClimatePresetModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;`

When the climate preset mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/development/sdk/device-attributes/#climateattribute) and the new value.

### `onClimateFanModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;`

When the climate fan mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/development/sdk/device-attributes/#climateattribute) and the new value.

### `onClimateSwingModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;`

When the climate swing mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/development/sdk/device-attributes/#climateattribute) and the new value.

### `onPowerChanged?(attribute: ClimateAttribute, value: boolean): Promise<void>;`

When the power state of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/development/sdk/device-attributes/#climateattribute) and the new value.

### `onTargetTemperatureChanged?(attribute: ClimateAttribute, value: number): Promise<void>;`

When the target temperature of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/development/sdk/device-attributes/#climateattribute) and the new value.

## Github

[device.ts](https://github.com/sorted-bits/quantumhub-sdk/blob/main/src/interfaces/device.ts).

