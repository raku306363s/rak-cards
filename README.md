# RAK Energy Card

A standalone Home Assistant Lovelace custom card for monitoring a three-phase electrical system.

This card is independently registered as `rak-energy-card` and does not register or overwrite the original Engineer Ismail card elements.

## Features

- Phase A, B and C power, voltage and current sensors
- Total live power calculated from the available phase power sensors
- Individual phase readings in the card details
- Optional total energy sensor
- Separate single-sensor RAK Power Card
- Editable watt thresholds and individual range colours for the Power Card
- Visual configuration editors
- HACS-compatible repository layout

## Installation

### HACS (custom repository)

1. Add this GitHub repository to HACS as an integration of type **Dashboard**.
2. Install **RAK Cards**.
3. Add the resource if HACS does not add it automatically:
   - URL: `/hacsfiles/rak-cards/rak-energy-card.js`
   - Resource type: `JavaScript Module`
4. Add the card to a dashboard using the YAML below.

## Card configuration

```yaml
type: custom:rak-energy-card
name: 3 Phase Energy
icon: mdi:lightning-bolt

power: sensor.spm02_wifi_power_a
voltage: sensor.spm02_wifi_phase_a_voltage
current: sensor.spm02_wifi_phase_a_current

power_b: sensor.spm02_wifi_power_b
voltage_b: sensor.spm02_wifi_phase_b_voltage
current_b: sensor.spm02_wifi_phase_b_current

power_c: sensor.spm02_wifi_power_c
voltage_c: sensor.spm02_wifi_phase_c_voltage
current_c: sensor.spm02_wifi_phase_c_current

energy: sensor.spm02_wifi_energy
max_power: 15000
```

### Sensor options

| Option | Description |
|---|---|
| `power`, `voltage`, `current` | Phase A power, voltage and current |
| `power_b`, `voltage_b`, `current_b` | Phase B power, voltage and current |
| `power_c`, `voltage_c`, `current_c` | Phase C power, voltage and current |
| `energy` | Optional total energy sensor |
| `max_power` | Total power in watts represented by a full dial (default: 15000 W) |

The total live power dial sums the configured phase power readings. The energy value is read from the single `energy` entity; it is not calculated by the card.

## Power-only card

Use `custom:rak-power-card` when you need a compact card for one power sensor. The dial colour changes automatically based on the configured watt ranges.

```yaml
type: custom:rak-power-card
name: Load Monitor
icon: mdi:flash
power: sensor.spm02_wifi_power_a

low_threshold: 50
high_threshold: 200
max_power: 3000

low_color: [22, 163, 74]
medium_color: [22, 163, 74]
high_color: [220, 38, 38]
```

The defaults are green below 50 W, green from 50 W through 200 W, and red above 200 W. You can edit both thresholds and each range colour in the visual card editor or YAML. The thresholds are in watts; the card also converts sensors reported in kW to watts for comparison and display. `max_power` controls the dial scale only.

| Option | Description | Default |
|---|---|---|
| `power` | Single power sensor | Required |
| `low_threshold` | Upper limit of the first range, in watts | `50` |
| `high_threshold` | Upper limit of the middle range, in watts | `200` |
| `low_color` | Colour below the low threshold | Green |
| `medium_color` | Colour between the thresholds, inclusive | Green |
| `high_color` | Colour above the high threshold | Red |
| `max_power` | Power represented by a full dial, in watts | `1000` |

Colours can be supplied as RGB arrays (for example `[22, 163, 74]`) or CSS hex colours (for example `"#16a34a"`).

## Attribution and license

This project is derived from **Engineer Ismail Cards**. The original MIT license and copyright notice are retained in `LICENSE`. The three-phase energy-card changes and independent RAK card packaging are modifications.