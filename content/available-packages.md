---
title: Available packages
type: default
toc: false
---

### Inverters

{{% details title="Afore AF XK-TH Inverter" closed="true" %}}

Available at [https://github.com/sorted-bits/modbus-solarman](https://github.com/sorted-bits/modbus-solarman).

```yaml
- package: afore
  identifier: quantumhub_afore_af_xk_th
  name: Afore AF XK-TH Inverter
  device: af-xk-th-three-phase-hybrid
  host: <ip address of the inverter>
  port: 8899
  unitId: 1
  updateInterval: 1
  solarman: false
```

{{% /details %}}

{{% details title="Growatt MID TL series" closed="true" %}}

Available at [https://github.com/sorted-bits/modbus-solarman](https://github.com/sorted-bits/modbus-solarman).

```yaml
- package: growatt-tl
  identifier: quantumhub_growatt_mid_tl
  name: Growatt MID TL series
  device: growatt-tl
  host: <ip address of the inverter>
  port: 502
  unitId: 1
  updateInterval: 1
  solarman: false
  unavailable_timeout: 180
```

{{% /details %}}


{{% details title="Growatt 3PH MOD TL3-X series" closed="true" %}}

Available at [https://github.com/sorted-bits/modbus-solarman](https://github.com/sorted-bits/modbus-solarman).

```yaml
- package: growatt-tl3-x
  identifier: quantumhub_growatt_3ph_mod_tl3_x
  name: Growatt 3PH MOD TL3-X series
  device: growatt-tl3
  host: <ip address of the inverter>
  port: 502
  unitId: 1
  updateInterval: 1
  solarman: false
  unavailable_timeout: 180
```

{{% /details %}}



