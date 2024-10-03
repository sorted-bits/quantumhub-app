---
title: Provider
type: docs
weight: 2
---

<style>
    h4 {
        opacity: 0.5;
        height: 0px;
        overflow: hidden;
        margin-top: 0px !important;
    }
</style>

<i class="fa-brands fa-github"></i> [Provider Interface](https://github.com/sorted-bits/quantumhub-sdk/blob/main/src/interfaces/provider.ts)

## Methods

#### setAttributeValue

```typescript
setAttributeValue(attribute: string, value: any): Promise<void>;
```

This will set the value of an attribute and publish it to the MQTT broker. The `attribute` is the name of the attribute as defined in the definition file of your package (optional).

#### setAvailability

```typescript
setAvailability(availability: boolean): Promise<void>;
```

This will set the availability of the device and publish the changes to MQTT. Setting `availability` to `false` will mark the device and any attributes having availability as `unavailable` in Home Assistant.

#### getConfig

```typescript
getConfig(): any;
```

This will return the configuration of the device as defined in the QuantumHub configuration file. It is returned as an object. 

## `provider.cache`

#### set

```typescript
set(key: string, value: any): Promise<void>;
```

Sets a value in the cache, linked to your device. This value will be saved in a SQLite database. The key needs to be unique, otherwise it will overwrite the existing value.

#### get

```typescript
get(key: string): Promise<any>;
```

Gets a value from the cache based on the provided key, if no value is found it will return `undefined`.

#### delete

```typescript
delete(key: string): Promise<void>;
```

Deletes a value from the cache based on the provided key.

#### all

```typescript
all(): Promise<{ [key: string]: any }>;
```

Gets all values from the cache as an object.

## `provider.timeout`

The timeout manager in the Provider is used to schedule tasks to run after a certain amount of time. This is useful for things like debouncing button presses or setting a value to an attribute after a certain amount of time. This uses the `setTimeout` and `clearTimeout` functions, but makes sure that the timeouts are cleared when the device is stopped/destroyed.

#### set

```typescript
set(callback: () => Promise<void>, timeout: number): NodeJS.Timeout;
```

#### clear

```typescript
clear(timeoutId: NodeJS.Timeout): Promise<void>;
```

## `provider.logger`

The logger is used to make sure that the device is able to log messages to the console but also when you are looking at the logs using the webinterface. Logged messages are not stored anywhere.

Make sure you select the log level, as this can easily cause a lot of log spam.

```typescript
trace(message: string): Promise<void>;
debug(message: string): Promise<void>;
info(message: string): Promise<void>;
warn(message: string): Promise<void>;
error(message: string): Promise<void>;
fatal(message: string): Promise<void>;
```

## `provider.mqtt`

This gives you access to the MQTT client that is used by QuantumHub.

#### subscribeToTopic

```typescript
subscribeToTopic(topic: string): Promise<void>;
```

Subscribe to a specific topic, this will trigger the `onMessage` [event on the device](/docs/sdk/device/#onmessagetopic-string-message-buffer-promisevoid).

#### publishToTopic

```typescript
publishToTopic(topic: string, message: string, retain: boolean): Promise<void>;
```

Allows you to manually publish a message to a specific topic.

## `provider.definition`

The `definition` object gives you access to the values you defined in your packages definition file.

```typescript
export interface Definition {
    path: string;

    name: string;
    entry: string;
    author?: string;
    description?: string;
    version?: string;

    attributes: Attribute[];
}
```
