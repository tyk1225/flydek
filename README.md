# FLYDEK

**A desk control panel for PC flight simulators, with a screen that draws the labels for its keys.**

<img width="2400" height="1350" alt="FLYDEK_cover_main" src="https://github.com/user-attachments/assets/891a45a5-313e-4bcf-8dba-52b9d660ea76" />


> Status: The PCB is designed, ordered and tested, the Pico is soldered, and firmware is next!

## What it is

FLYDEK v1 is a control deck that sits on your desk next to the keyboard while you fly. A 4-inch screen sits behind a window cut into the circuit board, with 6 keys above it and 6 keys below it. The keys have no printed labels: the screen draws each key's label right next to it, so the same 12 keys can do different jobs in each sim or aircraft profile.

On the left are two dual knobs (an outer ring and an inner knob, both with a push), for things you turn a lot, like heading and altitude. MASTER WARN and MASTER CAUT buttons with red and orange lights sit in the top-left corner, like in a real cockpit, and PROFILE and MENU buttons are on the right. A plug on the side (J4) is ready for a Lever Pack add-on with a gear lever and a flaps lever.

What makes it different: the labels change on the screen, and the plan is for FLYDEK to show up as a normal USB game controller and keyboard, so it needs no driver.

## How to use it

Firmware v1 is still being written, so this is how v1 is planned to work:

1. **Plug it in:** connect the Pico 2's USB port to your PC. FLYDEK shows up as a game controller and a keyboard.
2. **Pick a profile:** press **PROFILE** to switch between Desktop, Microsoft Flight Simulator and Roblox. The screen redraws all 12 key labels.
3. **Press a key:** each key sends the button or shortcut written next to it on the screen.
4. **Turn the knobs:** the outer ring and the inner knob each send their own inputs (for example heading and altitude), and pushing the knob is a third input.
5. **MENU:** opens settings on the screen (for example brightness).
6. **MASTER WARN / MASTER CAUT:** buttons you can map to your sim's warning controls; their lights are controlled by the firmware.

## How to build it

1. Order the PCB from the Gerbers in this repo (2-layer, 190 × 120 mm).
2. Buy the parts in `BOM.csv`.
3. Solder the low parts first: resistors, capacitors, the 28-pin socket for the MCP23017, then the two 20-pin sockets for the Pico 2, the screen header (J3) and the Lever Pack plug (J4) on the back.
4. Solder the 16 key switches, the 2 knobs and the 2 LEDs on the front.
5. Put the MCP23017 into its socket and the Pico 2 into its sockets.
6. Mount the screen behind the window on 4 mm spacers with M3 × 12 screws, and screw on the 4 × 35 mm brass legs.
7. Flash the firmware: hold BOOTSEL on the Pico 2, plug in USB, and drag the `.uf2` file onto the drive that appears.

## Why I made it

I fly Microsoft Flight Simulator and various flight sims on my PC, and pressing keyboard shortcuts in the middle of a flight breaks the feeling of flying a real plane. Ready-made sim panels I looked at cost about $130–180, and their buttons have fixed labels. My motto is "Don't buy it, make it", so I decided to design my own. FLYDEK started as an idea for a flight stick and turned into this deck. It's also my first real PCB: I wanted to learn how to design a circuit board from scratch, route every track myself and solder it together.

## Hardware (v1)

| Part | v1 |
|---|---|
| Board | 190 × 120 mm, 2-layer, through-hole, designed and routed by hand in KiCad 10 |
| Brain | Raspberry Pi Pico 2 in two 20-pin sockets on the back |
| Screen | 4.0" 480 × 320 SPI TFT (ST7796S, no touch), behind a window in the board |
| Keys | 16 × Omron B3F-4055: 12 softkeys around the screen, PROFILE, MENU, MASTER WARN, MASTER CAUT |
| Key reading | MCP23017 I/O expander (I2C) for the softkeys, PROFILE and MENU; WARN/CAUT on the Pico |
| Knobs | 2 × Bourns PEC11D dual concentric encoders with push |
| Lights | 2 × 3 mm LEDs (red WARN, orange CAUT) |
| Add-on port | J4 (JST XH 8-pin): gear up/off/down + I2C for the Lever Pack |
| Mounting | 4 × 35 mm brass M3 legs; screen on 4 mm spacers with M3 × 12 screws |

## Files

- KiCad project and Gerbers: this repo
- 3D model: `cad/FLYDEK-v1.step`
- Render: `images/FLYDEK-v1.png`
- Parts list with links and prices: `BOM.csv` (about $104 for one board)

## Status

- [x] Schematic and PCB designed in KiCad 10 (routed by hand)
- [x] 5 PCBs made by JLCPCB, beep-tested (17 Nov)
- [x] Pico 2 headers soldered and checked for shorts (20–21 Nov)
- [x] STEP with every 3D model
- [ ] Screen arrives (in customs, 22 Nov)
- [ ] Firmware v1: USB game controller + key labels on the screen
- [ ] Remaining parts, then solder and test the full board
- [ ] Lever Pack (subproject)

## Where FLYDEK is going (V4, later)

- My own RP2350B board instead of the Pico 2!
- Backlit black PCB faceplate and RGB light
- Lever Pack: spring-locked gear lever, clicking flaps lever
- Two screen themes (A-style and B-style)
- Web configurator for profiles and key labels
- Live sim data through MobiFlight

## AI use
Claude AI was used for research, 3d rendering, file management, and debugging

## Not affiliated

FLYDEK is an independent project. It is not made by or affiliated with Microsoft, Laminar Research, Boeing or Airbus. "Works with" mentions only describe compatibility.
