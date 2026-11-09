# FLYDEK

**A desk control panel for PC flight simulators.** The 12 keys around a 4-inch screen have no printed labels: the screen draws them, so every aircraft profile can rename every key. Two dual knobs, MASTER WARN / MASTER CAUT buttons, and a clip-on Lever Pack with a spring-locked gear lever and a clicking flaps lever complete the deck.

> Status: **design stage**. A hand-wired prototype is next. This is a Hack Club Forge project.

<!-- Add the cover image here once it's in the repo, e.g. ![FLYDEK V4](docs/flydek-v4.png) -->

## Why

- **Remembering what each control does is the most common complaint about generic sim panels.** FLYDEK shows the current label for every key on its screen, and the labels change when you switch profile or aircraft.
- **Many panels break after sim updates or need fiddly drivers.** FLYDEK aims to work with no driver, as a normal USB game controller.
- **Real cockpit feel on a desk:** knobs with click detents, a gear lever you pull to unlock, and a flaps lever that clicks into each notch.

## Features (V4 design)

### FLYDEK Core
- 4-inch 480 × 320 screen showing key labels, the profile name and live sim data
- 12 softkeys (6 above, 6 below the screen)
- 2 dual concentric knobs with push (4 functions)
- PROFILE and MENU buttons
- MASTER WARN and MASTER CAUT: half-transparent caps set into the deck, lit from below
- Black circuit-board faceplate with backlit lettering
- One USB-C cable to the PC, plus an add-on port

### Lever Pack (clips onto either side)
- Gear lever: UP / OFF / DN, pull to unlock, spring snaps it into each notch
- Flaps lever: a spring ball clicks into a curved gate; an AS5600 magnet sensor reads the angle
- Two swappable flaps gates: A-style (0, 1, 2, 3, FULL) and B-style (UP to 40 with gates at 1 and 15)
- 3 gear-down lights

### Screen themes
- **A-style:** narrow monospace font; green = engaged, cyan = values you set
- **B-style:** bold sans font; green = engaged, magenta = values you set

## Hardware

| Part | Choice |
| --- | --- |
| Microcontroller | Raspberry Pi RP2350B on FLYDEK's own 2-layer board (Raspberry Pi Pico 2 for the prototype) |
| Screen | 4.0" 480 × 320 SPI TFT, ST7796 driver |
| Knobs | 2 × Bourns PEC11D dual concentric encoders with push |
| Buttons | 16 tactile switches, read directly by the RP2350B |
| Lights | 25 × SK6812MINI-E RGB LEDs (through a 3.3 V → 5 V level shifter) |
| Flaps sensor | AS5600 magnetic angle sensor + diametric magnet |
| Gear sensing | 3 × Omron D2F-01L micro switches |
| Power | USB-C, 5.1 kΩ CC resistors, USBLC6-2SC6 ESD protection, polyfuse, AMS1117-3.3 |
| Case | Black PCB faceplate + 3D-printed tray with a steel weight + rubber feet |

Power budget: the screen and chips use about 270 mA, so LED brightness is capped (about 20% of full white) to stay inside USB 2.0's 500 mA.

## Software (planned)

- **Firmware:** Pico SDK + TinyUSB composite device (game controller + keyboard/media keys + a link for the web configurator), LVGL for the screen
- **Web configurator:** runs in Chrome or Edge over USB; profiles, key labels, actions and LED colours, saved on the deck
- **Live sim data:** through MobiFlight (FLYDEK registered as a custom board)
- **Sims:** Microsoft Flight Simulator 2020 and 2024, X-Plane 12

## Roadmap

- [x] Concept and four design versions (v1 → V4)
- [x] Research: parts, costs, competitors, manufacturing
- [ ] Screen layout prototype (LVGL)
- [ ] 3D-printed flaps lever to test the click
- [ ] Hand-wired prototype on a Pico 2 (screen, one dual knob, AS5600, buttons)
- [ ] Firmware: game controller + labels on the screen
- [ ] KiCad: RP2350B main board + faceplate
- [ ] First 5 boards from JLCPCB
- [ ] Live data through MobiFlight
- [ ] Test units with other sim players

## Prototype budget (Forge Tier 2, estimates)

| Item | About |
| --- | --- |
| 5 main boards, small parts soldered by JLCPCB, plus shipping | $90 |
| 4-inch ST7796 screen plus shipping | $20 |
| 2 × Bourns PEC11D dual encoders | $14 |
| AS5600 module + magnet | $7 |
| Tactile switches, caps, 3 micro switches | $8 |
| 5 black PCB faceplates (same order) | $20 |
| Screws, filament | $5 |
| **Total** | **about $165** |

## Repository layout (planned)

```
hardware/   KiCad files for the main board, faceplate and Lever Pack sensor board
firmware/   RP2350 firmware (Pico SDK, TinyUSB, LVGL)
case/       3D-print files for the tray, levers, gates and caps
docs/       Drawings, photos and notes
```

## AI use

Planning, research, and the concept drawings were made with help from Claude (an AI assistant), and this README was drafted with its help. The building, wiring, soldering, circuit-board layout and code are done by me.

## Not affiliated

FLYDEK is an independent project. It is not made by or affiliated with Microsoft, Laminar Research, Boeing or Airbus. "Works with" mentions only describe compatibility.
