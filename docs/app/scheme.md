# Config

## MQTT section

```yaml
mqtt:
  host:
  username:
  password:
  port:
  topic_prefix:
  ha_discovery:
```

```yaml
mqtt:
  type: dict
  required: True
  meta:
    label: Mqtt section
  schema:
    host:
      required: True
      type: string
      meta:
        label: Mqtt broker hostname or IP address
    username:
      required: True
      type: string
      meta:
        label: Username to connect ot mqtt broker
    password:
      required: False
      type: string
      meta:
        label: Password to mqtt
    port:
      required: True
      type: integer
      default: 1883
      meta:
        label: Port to connect to mqtt broker
    topic_prefix:
      type: string
      default: boneIO
      required: True
      meta:
        label: Prefix topic for boneIO to use
    ha_discovery:
      type: dict
      meta:
        label: Ha discovery sub section
      default: {}
      schema:
        enabled:
          type: boolean
          default: True
          meta:
            label: Enable HA discovery.
        topic_prefix:
          type: string
          default: homeassistant
          meta:
            label: Prefix topic of HA discovery.

oled:
  type: boolean
  coerce: to_bool

modbus:
  type: dict
  required: False
  schema:
    uart:
      type: string
      required: True
      meta:
        label: Uart ID to use

sdm630:
  type: list
  required: False
  meta:
    label: SDM630 sensor
  schema:
    type: dict
    schema:
      id:
        type: string
        required: False
        meta:
          label: Id of SDM630
      address:
        type: string
        required: True
        default: 0x33
        meta:
          label: Address of SDM to use.
      update_interval:
        type: integer
        required: True
        default: 30
        meta:
          label: Update interval in seconds.
lm75:
  type: dict
  required: False
  schema:
    id:
      type: string
      required: False
      meta:
        label: Id of I2C to use in pin config
    address:
      type: string
      required: True
      default: 0x48
      meta:
        label: GPIO of I2C SDA

mcp9808:
  type: dict
  required: False
  schema:
    id:
      type: string
      required: False
      meta:
        label: Id of I2C to use in pin config
    address:
      type: string
      required: True
      default: 0x18
      meta:
        label: GPIO of I2C SDA

mcp23017:
  type: list
  required: False
  meta:
    label: mcp23017 Pin config
  schema:
    type: dict
    schema:
      id:
        type: string
        required: True
        default: lm75
        meta:
          label: Id of I2C to use in pin config
      address:
        type: string
        required: True
        meta:
          label: GPIO of I2C SDA
      init_sleep:
        type: integer
        required: True
        default: 0
        meta:
          label: How long to sleep for MCP to initialize.

output:
  type: list
  meta:
    label: List of output relays
  check_with: output_id_uniqueness
  schema:
    type: dict
    schema:
      id:
        type: string
        required: False
        meta:
          label: Id to send to use in HA and in GPIO Input. Default to `kind_pin`
      kind:
        type: string
        allowed: ['gpio', 'mcp']
        meta:
          label: Either GPIO or i2c.
      mcp_id:
        type: string
        required: False
        meta:
          label: MCP ID to connect
      pin:
        type: string
        required: True
        meta:
          label: PIN to use.
      ha_type:
        type: string
        required: True
        allowed: ['switch', 'light']
        default: 'switch'
        meta:
          label: If HA discovery is used device if relay is light or switch.

input:
  type: list
  meta:
    label: GPIO inputs section
  schema:
    type: dict
    schema:
      id:
        type: string
        required: False
        meta:
          label: Id to use in HA if needed. Default to pin number.
      pin:
        type: string
        required: True
        meta:
          label: PIN to use.
      show_in_ha:
        type: boolean
        required: True
        default: True
        meta:
          label: If you want you can disable discovering this input in HA.
      kind:
        type: string
        allowed: ['switch', 'sensor']
        default: switch
        required: True
        meta:
          label: Either switch or sensor. If sensor then no clicks are detected, just simple on/off on gpio.
      actions:
        required: False
        type: dict
        schema:
          single:
            required: False
            type: dict
            schema:
              action:
                type: string
                allowed: ['mqtt', 'output']
                default: output
              pin:
                type: string
              message:
                type: string
          double:
            required: False
            type: dict
            schema:
              action:
                type: string
                allowed: ['mqtt', 'output']
                default: output
              pin:
                type: string
              message:
                type: string
          long:
            required: False
            type: dict
            schema:
              action:
                type: string
                allowed: ['mqtt', 'output']
                default: output
              pin:
                type: string
              message:
                type: string
          pressed:
            required: False
            type: dict
            schema:
              action:
                type: string
                allowed: ['mqtt', 'output']
                default: output
              pin:
                type: string
              message:
                type: string
          released:
            required: False
            type: dict
            schema:
              action:
                type: string
                allowed: ['mqtt', 'output']
                default: output
              pin:
                type: string
              message:
                type: string

adc:
  type: list
  meta:
    label: GPIO ADC section
  schema:
    type: dict
    schema:
      id:
        type: string
        required: False
        meta:
          label: Id to use in HA if needed. Default to pin number.
      pin:
        type: string
        required: True
        allowed: ['P9_33', 'P9_35', 'P9_36', 'P9_37', 'P9_38', 'P9_39', 'P9_40']
        meta:
          label: PIN to use.
      update_interval:
        type: integer
        required: True
        default: 60
        meta:
          label: Update interval in seconds.
      show_in_ha:
        type: boolean
        required: True
        default: True
        meta:
          label: If you want you can disable discovering this input in HA.
```
