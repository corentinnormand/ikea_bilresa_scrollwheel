# IKEA BILRESA Home Assistant Blueprints

Home Assistant blueprints for the IKEA BILRESA smart home devices.

## Blueprints

### 1. Scroll Wheel

Control brightness and color temperature with the scroll wheel. Supports multi-press acceleration and smooth transitions.

#### Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcorentinnormand%2Fikea_bilresa_scrollwheel%2Fmain%2Fikea_bilresa_scroll_wheel.yaml)

Or manually import:
```
https://raw.githubusercontent.com/corentinnormand/ikea_bilresa_scrollwheel/main/ikea_bilresa_scroll_wheel.yaml
```

#### Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| **Brightness: Scroll Right/Left Entity** | Event entities for brightness scroll | - |
| **Brightness: Button Press Entity** | Event entity for brightness toggle | - |
| **Brightness: Target Light** | Light to control | - |
| **Brightness: Increase/Decrease Step** | Brightness change per scroll (%) | 10% |
| **Brightness: Minimum** | Prevents turning off | 5% |
| **Brightness: Maximum** | Maximum brightness | 100% |
| **Temperature: Scroll Right/Left Entity** | Event entities for temperature scroll | - |
| **Temperature: Button Press Entity** | Event entity for temperature toggle | - |
| **Temperature: Target Light** | Light to control (must support color temp) | - |
| **Temperature: Increase/Decrease Step** | Temperature change per scroll (K) | 300K |
| **Temperature: Minimum Kelvin** | Warmest temperature | 2000K |
| **Temperature: Maximum Kelvin** | Coolest temperature | 6500K |
| **Transition Time** | Smoothing between values | 0.2s |
| **Automation Mode** | How to handle rapid scrolling | restart |

#### Example

```yaml
- id: 'bilresa_scroll_wheel_salon'
  alias: "BILRESA Scroll Wheel - Salon"
  use_blueprint:
    path: corentinnormand/ikea_bilresa_scroll_wheel.yaml
    input:
      # Brightness control (scroll wheel position 2)
      mode_1_scroll_right_entity: event.bilresa_scroll_wheel_bouton_4
      mode_1_scroll_left_entity: event.bilresa_scroll_wheel_bouton_5
      mode_1_button_press_entity: event.bilresa_scroll_wheel_bouton_6
      mode_1_target_light: light.salon
      mode_1_increase_brightness_step: 5
      mode_1_decrease_brightness_step: 5
      mode_1_min_brightness: 5
      # Temperature control (scroll wheel position 1)
      mode_2_scroll_right_entity: event.bilresa_scroll_wheel_bouton_1
      mode_2_scroll_left_entity: event.bilresa_scroll_wheel_bouton_2
      mode_2_button_press_entity: event.bilresa_scroll_wheel_bouton_3
      mode_2_target_light: light.salon
      mode_2_increase_temperature_step: 300
      mode_2_decrease_temperature_step: 300
      # Smoothing
      transition_time: 0.1
      automation_mode: restart
```

---

### 2. Dual Button

Control lights with single press, double press, and long press dimming.

#### Installation

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcorentinnormand%2Fikea_bilresa_scrollwheel%2Fmain%2Fikea_bilresa_dual_button.yaml)

Or manually import:
```
https://raw.githubusercontent.com/corentinnormand/ikea_bilresa_scrollwheel/main/ikea_bilresa_dual_button.yaml
```

#### Configuration

| Parameter | Description | Default |
|-----------|-------------|---------|
| **Button 1/2 Entity** | Event entities for each button | - |
| **Target Light** | Light to control | - |
| **Button 1: Single Press Action** | Action on single press | Turn On |
| **Button 1: Double Press Action** | Action on double press | Full Brightness |
| **Button 2: Single Press Action** | Action on single press | Turn Off |
| **Button 2: Double Press Action** | Action on double press | Dim (10%) |
| **Long Press Behavior** | Enable/disable dimming | Enabled |
| **Dimming Step** | Brightness change per step (%) | 10% |
| **Dimming Speed** | Delay between steps (ms) | 200ms |
| **Minimum Brightness** | Prevents turning off | 5% |
| **Maximum Brightness** | Maximum brightness | 100% |
| **Transition Time** | Smoothing between values | 0.2s |

#### Available Actions

| Action | Description |
|--------|-------------|
| `turn_on` | Turn light on |
| `turn_off` | Turn light off |
| `toggle` | Toggle light state |
| `full_brightness` | Set to 100% brightness |
| `dim_light` | Set to 10% brightness |
| `custom_brightness` | Set to custom brightness level |
| `warm_light` | Set to 2700K (warm white) |
| `cool_light` | Set to 5000K (cool white) |

#### Example

```yaml
- id: 'bilresa_dual_button_salon'
  alias: "BILRESA Dual Button - Salon"
  use_blueprint:
    path: corentinnormand/ikea_bilresa_dual_button.yaml
    input:
      button_1_entity: event.bilresa_dual_button_bouton_1
      button_2_entity: event.bilresa_dual_button_bouton_2
      target_light: light.salon
      button_1_single_action: turn_on
      button_1_double_action: warm_light
      button_2_single_action: turn_off
      button_2_double_action: cool_light
      dimming_step: 10
      min_brightness: 5
```

---

## Device Compatibility

These blueprints are designed for:
- **IKEA BILRESA Scroll Wheel** (E2201) - Matter/Zigbee
- **IKEA BILRESA Dual Button** (E2489) - Matter

## Troubleshooting

### Choppy/laggy scrolling
- Set `automation_mode` to `restart`
- Lower `transition_time` (try 0.1s or 0)
- Reduce step size for finer control

### Light turns off when dimming
- Increase `min_brightness` (default 5%)

### Multi-press not working
- Ensure your device firmware is up to date
- Check that `totalNumberOfPressesCounted` attribute is available

## License

MIT License - Feel free to use, modify, and share!
