# Split-Flap Card for Home Assistant

[![HACS Validation](https://github.com/RazManSource/splitflap-card/actions/workflows/validate.yml/badge.svg)](https://github.com/RazManSource/splitflap-card/actions/workflows/validate.yml)
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-41BDF5.svg)](https://github.com/hacs/integration)

A custom Lovelace card that turns your Home Assistant dashboard into a retro split-flap (flip-board) display — the kind you'd see at airports and train stations. Push messages to it from any automation.

Inspired by [FlipOff](https://github.com/magnum6actual/flipoff), a free split-flap display emulator.

![Split-Flap Card Demo](splitflap.gif)

## Features

- Realistic split-flap scramble animation — only tiles that change will flip
- Synthesised mechanical flap sound (two types: mechanical and soft)
- Driven by any entity — `input_text`, template sensors, or anything with a text state
- Customisable fonts (Google Fonts supported) and font weight
- Random colour mode — each tile keeps a colour from the palette
- Configurable accent bars (rainbow, solid, or off) and background colour
- Animation on/off toggle for e-ink displays
- Visual config editor with entity search — no YAML required
- Fully local — no cloud, no subscriptions, no external dependencies

## Installation

### HACS (Recommended)

[![Open your Home Assistant instance and open a repository inside the Home Assistant Community Store.](https://my.home-assistant.io/badges/hacs_repository.svg)](https://my.home-assistant.io/redirect/hacs_repository/?owner=RazManSource&repository=splitflap-card&category=plugin)

Or manually:

1. Open HACS in Home Assistant
2. Click the three dots in the top right → **Custom repositories**
3. Add `https://github.com/RazManSource/splitflap-card` with category **Dashboard**
4. Search for "Split-Flap" and click **Install**
5. Restart Home Assistant

### Manual

1. Download `splitflap-card.js` from the [latest release](https://github.com/RazManSource/splitflap-card/releases/latest)
2. Copy it to your Home Assistant `/config/www/` folder
3. Add it as a resource:
   - Go to **Settings → Dashboards → ⋮ (top right) → Resources**
   - Click **Add Resource**
   - URL: `/local/splitflap-card.js`
   - Type: **JavaScript Module**
4. Hard refresh your browser (Ctrl+F5)

### Create an input_text helper

- Go to **Settings → Devices & Services → Helpers → Create Helper → Text**
- Name it whatever you like (e.g. "Splitflap Message")
- Set max length to **132** (6 rows × 22 columns)

## Configuration

All options are available in the **visual editor** — no YAML needed. The entity field has a searchable dropdown of all your entities.

### Minimal

```yaml
type: custom:splitflap-card
entity: input_text.splitflap_message
```

### Full options

```yaml
type: custom:splitflap-card
entity: input_text.splitflap_message
title: ""                    # optional heading above the board
rows: 6                      # default 6
columns: 22                  # default 22

# Appearance
font_family: "Courier New"   # any system font or Google Font (see list below)
font_weight: "bold"          # "light", "normal", "bold", "extra-bold"
font_size: auto              # "auto" scales to card width, or a fixed value e.g. "24px"
accent_color: "#e8572a"      # accent colour used by bars
background_color: "#1a1a1a"  # board background colour, or "transparent"
bar_style: "rainbow"         # "rainbow" (multicolour), "solid" (accent colour), "off" (hidden)
color_mode: "default"        # "default" (dark tiles) or "random" (each tile keeps a colour)
scramble_colors:             # colours used during scramble and by random colour mode
  - "#e8572a"
  - "#f5a623"
  - "#4a90d9"
  - "#7ed321"
  - "#bd10e0"

# Animation
animation: true              # set false for e-ink displays (instant update, no scramble)
scramble_duration: 600       # ms — how long each tile scrambles before settling
stagger_delay: 25            # ms — delay between each tile starting its animation

# Sound
sound: false                 # enable flip sound (default off)
sound_type: "mechanical"     # "mechanical" (click + flutter + thud) or "soft" (gentle clack)
sound_delay: 0               # ms offset to shift sound timing vs animation (can be negative)
sound_every: 3               # play a sound every N tiles (1 = every tile, 3 = every 3rd)

# Text
word_wrap: true              # wrap long text across rows
line_separator: "|"          # character to force a new line in messages
```

### Font presets

The following fonts are available in the editor dropdown. Google Fonts are loaded automatically:

| Font | Type |
|------|------|
| Courier New | System |
| Consolas | System |
| Roboto Mono | Google Font |
| JetBrains Mono | Google Font |
| Fira Mono | Google Font |
| Source Code Pro | Google Font |
| IBM Plex Mono | Google Font |
| Space Mono | Google Font |
| Ubuntu Mono | Google Font |
| PT Mono | Google Font |

Select **Custom...** in the dropdown to enter any other font name (system or Google Font).

### Sound note

Browsers block auto-playing audio until the user interacts with the page. On a wall-mounted tablet, tap the card once to unlock audio — after that, sounds will play automatically on every message change.

### Entity types

The card works with any entity that has a text state, not just `input_text` helpers. You can also use template sensors to build dynamic messages:

```yaml
template:
  - sensor:
      - name: "Splitflap Weather"
        state: >
          {{ now().strftime('%A').upper() }} {{ now().strftime('%H:%M') }}|{{ states('sensor.outside_temperature') | round(0) }} DEGREES OUTSIDE
```

Then point the card at `sensor.splitflap_weather`.

## Pushing messages

The card watches the entity you configure. To change what's displayed, just set its value. Use `|` for line breaks.

### From the UI

Go to **Developer Tools → Services** and call:

```yaml
service: input_text.set_value
target:
  entity_id: input_text.splitflap_message
data:
  value: "HELLO WORLD"
```

### From automations

#### Morning weather greeting

```yaml
automation:
  - alias: "Splitflap Morning Weather"
    trigger:
      - platform: time
        at: "07:00:00"
    action:
      - service: input_text.set_value
        target:
          entity_id: input_text.splitflap_message
        data:
          value: >-
            GOOD MORNING|IT IS {{ states('sensor.outside_temperature') | round(0) }} DEGREES|OUTSIDE TODAY
```

#### Doorbell alert

```yaml
  - alias: "Splitflap Doorbell"
    trigger:
      - platform: state
        entity_id: binary_sensor.front_door_motion
        to: "on"
    action:
      - service: input_text.set_value
        target:
          entity_id: input_text.splitflap_message
        data:
          value: "SOMEONE IS|AT THE DOOR"
```

#### Live sensor display

```yaml
  - alias: "Splitflap Live Temp"
    trigger:
      - platform: state
        entity_id: sensor.outside_temperature
    action:
      - service: input_text.set_value
        target:
          entity_id: input_text.splitflap_message
        data:
          value: >-
            {{ now().strftime('%A').upper() }} {{ now().strftime('%H:%M') }}|{{ states('sensor.outside_temperature') | round(0) }} DEGREES OUTSIDE
```

Any automation that can call `input_text.set_value` can push messages to the board — weather, calendar events, appliance notifications, solar generation, you name it.

## Updating

When you replace the JS file, your browser may cache the old version. To force a reload, add a version query string to your resource URL:

```
/local/splitflap-card.js?v=2
```

Bump the number each time you update the file, then hard refresh (Ctrl+F5) your dashboard.

## Credits

- Inspired by [FlipOff](https://github.com/magnum6actual/flipoff) by magnum6actual
- Built with the help of [Claude](https://claude.ai) by Anthropic

## License

MIT
