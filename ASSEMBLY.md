# Assembly

A detailed guide to assemble the hermes handheld gaming console from 3d Printed parts, handwiring and other components.

---

## Before You Start

### Tools Required
- Soldering iron + solder
- Wire strippers
- Small screwdriver (M2)
- Hot glue gun or Superglue
- Multimeter (recommended for checking connections optional tho)
- Helping hands / PCB holder (optional but useful for soldering)

### Parts Required
Refer to [bom/bom.md](bom/bom.md) for the full bill of materials. in brief you will need these:

| Part | Qty |
|---|---|
| Raspberry Pi Zero 2W | 1 |
| Waveshare 5" HDMI Display | 1 |
| Adafruit PowerBoost 1000C | 1 |
| LiPo Battery 3000mAh (3.7V, 60×50mm) | 1 |
| Tactile switches (6×6×5mm) | 10 |
| 3.5mm audio jack | 1 |
| Slide switch (SPDT) | 1 |
| Jumper wires | several |
| M2 screws | 4 |

### 3D Printed Parts Required
Print all STLs from the `/cad` folder before starting. Recommended settings: 0.2mm layer height, 20% infill, PLA.

| File | Qty |
|---|---|
| `bottom_shell_ds.stl` | 1 |
| `top_shell_ds.stl` | 1 |
| `abxy_button.stl` | 6 |
| `dpad.stl` | 1 |
| `power_button.stl` | 1 |

---

## Soldering Headers onto the Pi Zero 2W

if the pi zero 2w ships without headers we need to add the header pins to it 
1. Place the 40-pin male header into the Pi Zero 2W GPIO holes.
2. Solder each pin carefully making sure there are no bridges between adjacent pins.
3. Let it cool completely and properly
---

## Preparing the PowerBoost 1000C

1. Solder short jumper wires to the following PowerBoost pads:
   - **BAT+** and **BAT−** to for the LiPo battery
   - **5V** and **GND** to for powering the Pi Zero 2W
   - **EN** to the slide switch (used for power on/off)
2. Solder two wires to the slide switch and connect one end to the **EN** pad on the PowerBoost and the other to **GND** when the switch breaks the EN–GND connection the PowerBoost will turn off

---

## Wiring the Battery

1. Connect the LiPo battery's JST connector to the **BAT** port on the PowerBoost 1000C.
   - If no JST connector solder the red wire to **BAT+** and black wire to **BAT−**.
2. Double check the polarity with a multimeter before connecting or it might damage components

---

## Connecting the Pi Zero 2W to the PowerBoost

1. Solder or use jumper wires to connect:
   - PowerBoost **5V** to Pi Zero 2W **Pin 2 (5V)**
   - PowerBoost **GND** to Pi Zero 2W **Pin 6 (GND)**
2. now we can do a quick power test: flip the slide switch and verify the Pi boots (green LED on Pi should blink :3)

---

## Connecting the Display

1. Connect the Waveshare 5" display to the Pi Zero 2W using the Mini HDMI cable/adapter.
2. The display also needs power  connect its **5V** and **GND** pins to the Pi's **5V** and **GND** pins (or tap off the PowerBoost output).
3. Refer to the schematic PDF in `/schematics` for exact pin labeling.

---

## Wire the Buttons

All 10 tactile switches use the Pi Zero 2W's internal pull-ups  no external resistors are needed.
Wire each button between its GPIO pin and **GND** (Pin 14 or any GND pin). The Pi will read LOW when a button is pressed.

| Button | GPIO Pin |
|---|---|
| A | GPIO 17 |
| B | GPIO 27 |
| X | GPIO 22 |
| Y | GPIO 10 |
| Start | GPIO 9 |
| Select | GPIO 11 |
| D-Pad Up | GPIO 5 |
| D-Pad Down | GPIO 6 |
| D-Pad Left | GPIO 13 |
| D-Pad Right | GPIO 19 |

> These pin assignments are based on the KiCad schematic Confirm against `/schematics` before soldering.

1. Solder one leg of each tactile switch to its GPIO wire and the other leg to a shared GND wire
2. Keep wires as short as practical so everything fits inside the shell

---

## Wiring the Audio Jack

1. Connect the 3.5mm audio jack to **GPIO 18** on the Pi Zero 2W (PWM audio output).
2. Also connect the jack's ground sleeve to Pi **GND**.
3. PWM audio requires a simple RC filter for acceptable quality a 270 ohm resistor in series and a 33nF capacitor to ground on each channel is recommended, though optional for basic testing.

---

## Seat Components into the Bottom Shell

The bottom shell (195×100×15mm) houses all the internals.

1. Place the **LiPo battery** flat in the center/lower area of the bottom shell.
2. Place the **PowerBoost 1000C** in the upper-left corner near the MicroUSB charging cutout.
3. Place the **Pi Zero 2W** in the remaining space, with the GPIO pins facing inward.
4. Slide the **slide switch** into the 8×4mm cutout on the side wall.
5. Fit the **MicroUSB port** of the PowerBoost through the 9×4.5mm cutout on the side wall.
6. Use hot glue sparingly to tack components in place if needed.

> Make sure no wires are pinched against the walls before closing the shell.

---

## Seat the Buttons into the Top Shell

1. Drop each **ABXY button** into its corresponding hole on the right side of the top shell.
2. Place the **D-Pad** into the left-side cutout.
3. Insert **Start** and **Select** buttons into the bottom center cutouts.
4. Press the **power button** into the side cutout.
5. The tactile switches sit underneath each button cap make sure they are aligned so pressing each cap actuates the switch directly below.

---

## Mounting the Display

1. Slide the **Waveshare 5" display** into the screen cutout on the top shell from the inside.
2. The display should sit flush with the front face of the shell.
3. Use hot glue to keep it in place if loose but it should be perfectly fit as the measurments are accurate

---

## Closing the Shell

1. Carefully fold all wires into the bottom shell so nothing comes out
2. Insert an M2 nut into the top shell hole from the inside before closing
3. Push an M2 screw up through the bottom shell from the outside
4. The screw threads into the nut inside the top shell, clamping them together
5. The nut might need a tiny dab of hot glue to stop it spinning while you screw in

---

## Power On and Test

1. Flip the slide switch to power on.
2. Verify:
   - [ ] Display turns on and shows Pi boot screen
   - [ ] All 10 buttons register input (test with a simple GPIO script)
   - [ ] Audio jack produces sound
   - [ ] MicroUSB charges the battery (PowerBoost LED should indicate charging)
3. If anything does not work, open the shell and re-check the relevant wiring against the schematic in `/schematics`.

---

Once assembled, flash your MicroSD card with your OS of choice (RetroPie, Batocera, or Raspberry Pi OS i aint planning for a custom firmware right now) and configure button mappings in your emulator frontend.

Refer to [JOURNAL.md](JOURNAL.md) for the full build log
