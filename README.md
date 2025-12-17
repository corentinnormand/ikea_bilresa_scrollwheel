# IKEA Bilresa Scroll Wheel – Simple Brightness Control

A Home Assistant blueprint for controlling light brightness using the IKEA Bilresa scroll wheel.

## Features

- **Scroll** to adjust brightness (configurable step size)
- **Press** to toggle light on/off
- Configurable scroll direction (increase/decrease)
- Queued mode for smooth scrolling

## Installation

Click the badge below to import this blueprint into your Home Assistant instance:

[![Open your Home Assistant instance and show the blueprint import dialog with a specific blueprint pre-filled.](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fraw.githubusercontent.com%2Fcorentinnormand%2Fikea_bilresa_scrollwheel%2Fmain%2Fikea_bilresa_scroll_wheel.yaml)

Or manually import using this URL:
```
https://raw.githubusercontent.com/corentinnormand/ikea_bilresa_scrollwheel/main/ikea_bilresa_scroll_wheel.yaml
```

## Configuration

After importing the blueprint, you'll need to configure:

1. **Scroll Right Entity** - The event entity for scroll right actions
2. **Scroll Left Entity** - The event entity for scroll left actions
3. **Button Press Entity** - The event entity for button press actions
4. **Target Light** - The light to control
5. **Brightness Steps** - How much to increase/decrease per scroll (1-50%)
6. **Scroll Direction** - Whether scrolling right increases or decreases brightness
