# A component for a Lasko S18708 DC Motor 18" pedestal fan.
The infrared sensor was removed, and an ESP-WROOM32 was soldered where the old infrared receiver was.
The ESP32 controls the fan using infrared remote commands, and can read the speed and oscillation by
monitoring the respective status pins.

This component requires a configured `duty_cycle` sensor and a `remote_transmitter`.

Example:
```yaml
external_components:
  - source:
      type: git
      url: https://github.com/fuxxociety/esphome_components
      ref: fan
    refresh: 0s

remote_transmitter:
  id: remote
  pin:
    number: GPIO32
    inverted: true
  carrier_duty_percent: 100%

sensor:
  - platform: duty_cycle
    id: fanspeed
    pin:
      number: GPIO17
      mode:
        input: True
        pullup: false

fan:
  - platform: pedestal
    name: Pedestal Fan
    pulse: fanspeed
    osc_pin: GPIO16
    transmitter_id: remote
```
