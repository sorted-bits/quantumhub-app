---
title: Provider
type: docs
weight: 2
---

## Methods

#### `setAttributeValue(attribute: string, value: any): Promise<void>;`
#### `setAvailability(availability: boolean): Promise<void>;`
#### `getConfig(): any;`

## provider.cache

#### `set(key: string, value: any): Promise<void>;`
#### `get(key: string): Promise<any>;`
#### `delete(key: string): Promise<void>;`
#### `all(): Promise<{ [key: string]: any }>;`

## provider.timeout

#### `set(callback: () => Promise<void>, timeout: number): NodeJS.Timeout;`
#### `clear(timeoutId: NodeJS.Timeout): Promise<void>;`

## provider.logger

#### `trace(message: string): Promise<void>;`
#### `debug(message: string): Promise<void>;`
#### `info(message: string): Promise<void>;`
#### `warn(message: string): Promise<void>;`
#### `error(message: string): Promise<void>;`
#### `fatal(message: string): Promise<void>;`

## provider.mqtt

#### `subscribeToTopic(topic: string): Promise<void>;`

#### `publishToTopic(topic: string, message: string, retain: boolean): Promise<void>;`

## provider.definition

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
