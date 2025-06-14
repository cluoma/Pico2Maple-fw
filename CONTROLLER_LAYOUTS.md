# Custom Controller Layouts/Remappings

Pico2Maple has a flexible controller remapping system which allows basically an entire controller to be remapped.

This feature currently requires an SD card attached to the device to load a mapping. However, once the custom layout is loaded, the SD card is no longer needed. A current goal is to find a convenient solution to load custom layouts without the need for an SD card. If you have suggestions, feel free to reach out.

## The Remapping File

### File Location

Pico2Maple will attempt to parse a controller layout from a file named `pico2maple_controller_map.cfg` placed in the `pico2maple` directory of the SD card.

If no file is found, a skeleton remapping file will be created called `pico2maple_controller_map_sample.cfg`. This is a good starting point to create your own mapping. Just remove the `_sample` from the end of the file and Pico2Maple will use it.

### File Layout

A remapping config file is a list of mappings, one per line. If a line begins with a hash symbol (`#`), it will be ignored.

Each line should be in the format: \<input\>: \<output\>

Where \<input\> is the name of the input button and <output> is the name of the output button.

Available **inputs** are standard Xbox-style gamepad buttons:

* `A, B, X, Y, LB, RB, LT, RT, START`
* `A1_UP/DOWN/LEFT/RIGHT, A2_UP/DOWN/LEFT/RIGHT`
* `DPAD_UP/DOWN/LEFT/RIGHT`

Available **outputs** are any Dreamcast controller buttons:

* `A, B, X, Y, LT, RT, START, C, Z, D`
* `A1_UP/DOWN/LEFT/RIGHT, A2_UP/DOWN/LEFT/RIGHT`
* `DPAD_UP/DOWN/LEFT/RIGHT, DPAD2_UP/DOWN/LEFT/RIGHT`

### Example Remapping File

An example of remapping that simply swaps the `A/B` and `X/Y` buttons, and is loaded by default, looks like this:

```txt
# Standard Dreamcast mapping with Nintendo facebutton layout
A: B
B: A
X: Y
Y: X
LT: LT
RT: RT
START: START
A1_UP: A1_UP
A1_DOWN: A1_DOWN
A1_LEFT: A1_LEFT
A1_RIGHT: A1_RIGHT
DPAD_UP: DPAD_UP
DPAD_DOWN: DPAD_DOWN
DPAD_LEFT: DPAD_LEFT
DPAD_RIGHT: DPAD_RIGHT
OPTION_AUTOLOAD: TRUE
```

## Limitations

* Any input can be mapped to any output.
* Up to 4 inputs can be mapped to same output. E.g. `RB` and `LB` could both map to `B`.
    * When multiple inputs map to the same output, the value of the output is determined in an OR fashion. E.g. `B` will be pressed if either `RB` *OR* `LB` is pressed.
* The same input may be mapped to multiple outputs. E.g. `DPAD_UP` could activate both `A1_UP` *and* `DPAD_UP`.
* Analog axis for LEFT/RIGHT and UP/DOWN will cancel each other out if both are activated.

Any custom mapping targeting a non-standard Dreamcast button such as `C`, `Z`, the second analog etc., will cause Pico2Maple to report itself to the Dreamcast as a controller that has all these buttons. Some games do not like this and will refuse to recognize the controller. A custom mapping that only targets buttons on a standard Dreamcast controller will cause Pico2Maple to show up as a standard controller to the Dreamcast and will avoid this issue.

## Options

Options in remapping files follow the same format as buttons, e.g. `OPTION_AUTOLOAD: TRUE`.

### Autoload

`OPTION_AUTOLOAD: FALSE/TRUE`

This option tells Pico2Maple whether or not this layout should be loaded automatically. Normally a standard controller is used
