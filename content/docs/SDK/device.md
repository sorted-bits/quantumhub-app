---
title: Device
type: docs
weight: 1
---

<style>
    h4 {
        opacity: 0.5;
        height: 0px;
        overflow: hidden;
        margin-top: 0px !important;
    }
</style>

## Required methods

#### init
```typescript
init(provider: Provider): Promise<boolean>;
```

Called after the package is loaded from disk and the [`Provider`](/docs/sdk/provider/) for your device is initialized. This [`Provider`](/docs/sdk/provider/) gives you access to all the exposed features of QuantumHub, so you'll probably want to store it in your device class. 

You can return false if something goes wrong, in that case the device will be disabled in the UI and there will be no attempt to start your device.

#### start
```typescript
start(): Promise<void>;
```

Called when the device is being started, during startup this is immediately after the init method (if the device isn't disabled in the config, and init passed succesfully). 

This is method returns a promise, but QuantumHub will not wait for it to finish, it will continue starting other devices. 

#### stop
```typescript
stop(): Promise<void>;
```

Called when the device is being stopped. This is only called when the device is stopped using the stop button in the QuantumHub UI or when QuantumHub is shutting down.

#### destroy
```typescript
destroy(): Promise<void>;
```

Called when the device is being destroyed. This is only called when QuantumHub is shutting down.

#### valueChanged
```typescript
valueChanged(attribute: Attribute, value: any): Promise<void>;
```

Called when the value of an [`Attribute`](/docs/sdk/device-attributes/) is changed, for example a value is changed by the Home Assistant MQTT integration.


## Optional methods

### MQTT

#### onMessage
```typescript
onMessage?(topic: string, message: Buffer): Promise<void>;
```

When your device is manually subscribed to a topic on the MQTT broker, this method is called when a new value is received on that topic.

Check out [`provider.mqtt.subscribeToTopic`](/docs/sdk/provider/#subscribetotopictopic-string-promisevoid) for more information.

### Scene

#### onSceneTriggered
```typescript
onSceneTriggered?(attribute: SceneAttribute): Promise<void>;
```

When your device exposes a scene to Home Assistant, this method is called when the scene is triggered. The supplied parameter contains the triggered [`SceneAttribute`](/docs/sdk/device-attributes/#sceneattribute).

### Button

#### onButtonPressed
```typescript
onButtonPressed?(attribute: ButtonAttribute): Promise<void>;
```

When your device exposes a button to Home Assistant, this method is called when the button is pressed. The supplied parameter contains the triggered [`ButtonAttribute`](/docs/sdk/device-attributes/#buttonattribute).

### Select

#### onSelectChanged
```typescript
onSelectChanged?(attribute: SelectAttribute, value: string): Promise<void>;
```

When the value of a select attribute is changed, this method is called. The supplied parameter contains the changed [`SelectAttribute`](/docs/sdk/device-attributes/#selectattribute) and the selected value, which is supplied in the `options` field of the attribute.

### Number

#### onNumberChanged
```typescript
onNumberChanged?(attribute: NumberAttribute, value: number): Promise<void>;
```

When the value of a number attribute is changed, this method is called. The supplied parameter contains the changed [`NumberAttribute`](/docs/sdk/device-attributes/#numberattribute) and the new value.

### Switch

#### onSwitchChanged
```typescript
onSwitchChanged?(attribute: SwitchAttribute, value: boolean): Promise<void>;
```

When the value of a switch attribute is changed, this method is called. The supplied parameter contains the changed [`SwitchAttribute`](/docs/sdk/device-attributes/#switchattribute) and the new value.

### Climate

#### onHvacModeChanged
```typescript
onHvacModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;
```

When the hvac mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.

#### onClimateModeChanged
```typescript
onClimateModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;
```

When the climate mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.

#### onClimatePresetModeChanged
```typescript
onClimatePresetModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;
```

When the climate preset mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.

#### onClimateFanModeChanged
```typescript
onClimateFanModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;
```

When the climate fan mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.

#### onClimateSwingModeChanged
```typescript
onClimateSwingModeChanged?(attribute: ClimateAttribute, value: string): Promise<void>;
```

When the climate swing mode of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.

#### onPowerChanged
```typescript
onPowerChanged?(attribute: ClimateAttribute, value: boolean): Promise<void>;
```

When the power state of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.

#### onTargetTemperatureChanged
```typescript
onTargetTemperatureChanged?(attribute: ClimateAttribute, value: number): Promise<void>;
```

When the target temperature of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.

#### onTargetHumidityChanged
```typescript
onTargetHumidityChanged?(attribute: ClimateAttribute, value: number): Promise<void>;
```

When the target humidity of a climate attribute is changed, this method is called. The supplied parameter contains the changed [`ClimateAttribute`](/docs/sdk/device-attributes/#climateattribute) and the new value.


