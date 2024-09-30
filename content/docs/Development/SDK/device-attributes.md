---
title: Attributes
type: docs
weight: 3
---

# Attributes

### `BaseAttribute`

```typescript
export interface BaseAttribute {
  // The unique key for this attribute. This should be unique per device.
  key: string;
  // The type of device this attribute belongs to.
  type: DeviceType;
  // The name of the attribute.
  name: string;
  // The device class of the attribute.
  device_class?: DeviceClass;
  // The unit of measurement of the attribute.
  unit_of_measurement?: string;
  // The state class of the attribute.
  state_class?: string;
  // If the attribute has availability.
  availability?: boolean;
  // The value that is stored when the attribute is unavailable.
  unavailability_value?: string;
}
```

### `SceneAttribute`

```typescript
export interface SceneAttribute extends BaseAttribute {
  type: DeviceType.scene;
}
```

### `DeviceTrackerAttribute`
```typescript
export interface DeviceTrackerAttribute extends BaseAttribute {
  type: DeviceType.device_tracker;
  source_type?: 'gps' | 'router' | 'bluetooth' | 'bluetooth_le';
}
```

### `SwitchAttribute`
```typescript
export interface SwitchAttribute extends BaseAttribute {
  type: DeviceType.switch;
  optimistic: boolean;
}
```

### `NumberAttribute`
```typescript
export interface NumberAttribute extends BaseAttribute {
  type: DeviceType.number;
  min: number;
  max: number;
  step: number;
}
```

### `SelectAttribute`
```typescript
export interface SelectAttribute extends BaseAttribute {
  type: DeviceType.select;
  optimistic: boolean;
  options: string[];
}
```

### `ClimateAttribute`
```typescript
export interface ClimateAttribute extends BaseAttribute {
  type: DeviceType.climate;
  optimistic: boolean;
  has_fanmode: boolean;
  has_swingmode: boolean;
  has_presetmode: boolean;
  has_humidity_control: boolean;
}
```
