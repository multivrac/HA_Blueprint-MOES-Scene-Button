# HA_Blueprint-MOES-Scene-Button
**manufacturer: _TZ3000_wkai4ga5**

**model: TS0044**

MOES TUYA Zigbee scene Button - Blueprint for Home Assistant

Code du fichier YAML:

```
blueprint:
  name: ZHA - Tuya 4-Button Scene Switch MOES
  description: Automate your Tuya 4-Button Scene Switch using ZHA events.
  domain: automation
  input:
    tuya_4button_scene_switch:
      name: Tuya 4-Button Scene Switch
      description: Tuya 4-Button Scene Switch to use
      selector:
        device:
          integration: zha
          manufacturer: _TZ3000_wkai4ga5
          model: TS0044
          multiple: false
    button_one_short_press:
      name: Single Press
      description: Action to run on button 1 (Upper-left) single press
      default: []
      selector:
        action: {}
    button_one_double_press:
      name: Double Press
      description: Action to run on button 1 (Upper-left) double press
      default: []
      selector:
        action: {}
    button_one_long_press:
      name: Long Press
      description: Action to run on button 1 (Upper-left) long press
      default: []
      selector:
        action: {}
    button_two_short_press:
      name: Single Press
      description: Action to run on button 2 (Upper-right) single press
      default: []
      selector:
        action: {}
    button_two_double_press:
      name: Double Press
      description: Action to run on button 2 (Upper-right) double press
      default: []
      selector:
        action: {}
    button_two_long_press:
      name: Long Press
      description: Action to run on button 2 (Upper-right) long press
      default: []
      selector:
        action: {}
    button_three_short_press:
      name: Single Press
      description: Action to run on button 3 (Lower-left) single press
      default: []
      selector:
        action: {}
    button_three_double_press:
      name: Double Press
      description: Action to run on button 3 (Lower-left) double press
      default: []
      selector:
        action: {}
    button_three_long_press:
      name: Long Press
      description: Action to run on button 3 (Lower-left) long press
      default: []
      selector:
        action: {}
    button_four_short_press:
      name: Single Press
      description: Action to run on button 4 (Lower-right) single press
      default: []
      selector:
        action: {}
    button_four_double_press:
      name: Double Press
      description: Action to run on button 4 (Lower-right) double press
      default: []
      selector:
        action: {}
    button_four_long_press:
      name: Long Press
      description: Action to run on button 4 (Lower-right) long press
      default: []
      selector:
        action: {}
  source_url: https://github.com/multivrac/HA_Blueprint-MOES-Scene-Button
mode: restart
max_exceeded: silent
trigger:
- platform: event
  event_type: zha_event
  event_data:
    device_id: !input 'tuya_4button_scene_switch'
action:
- variables:
    command: '{{ trigger.event.data.command }}'
    endpoint_id: '{{ trigger.event.data.endpoint_id }}'
- choose:
  - conditions: '{{ command == ''remote_button_short_press'' }}'
    sequence:
    - choose:
      - conditions: '{{ endpoint_id == 1 }}'
        sequence: !input 'button_one_short_press'
      - conditions: '{{ endpoint_id == 2 }}'
        sequence: !input 'button_two_short_press'
      - conditions: '{{ endpoint_id == 3 }}'
        sequence: !input 'button_three_short_press'
      - conditions: '{{ endpoint_id == 4 }}'
        sequence: !input 'button_four_short_press'
  - conditions: '{{ command == ''remote_button_double_press'' }}'
    sequence:
    - choose:
      - conditions: '{{ endpoint_id == 1 }}'
        sequence: !input 'button_one_double_press'
      - conditions: '{{ endpoint_id == 2 }}'
        sequence: !input 'button_two_double_press'
      - conditions: '{{ endpoint_id == 3 }}'
        sequence: !input 'button_three_double_press'
      - conditions: '{{ endpoint_id == 4 }}'
        sequence: !input 'button_four_double_press'
  - conditions: '{{ command == ''remote_button_long_press'' }}'
    sequence:
    - choose:
      - conditions: '{{ endpoint_id == 1 }}'
        sequence: !input 'button_one_long_press'
      - conditions: '{{ endpoint_id == 2 }}'
        sequence: !input 'button_two_long_press'
      - conditions: '{{ endpoint_id == 3 }}'
        sequence: !input 'button_three_long_press'
      - conditions: '{{ endpoint_id == 4 }}'
        sequence: !input 'button_four_long_press'
```
