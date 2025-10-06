# Pico2Maple - Custom Controller Layouts/Remappings

Pico2Maple has a flexible controller remapping system which allows basically an entire controller to be remapped.

There are currently two methods for loading a custom mapping to a Pico2Maple device. A config file can be loaded from a connected SD card, or a mapping can be uploaded directly using `picotool`.

Once loaded, a custom layout can be activated by pressing **Select + Dpad Right**.

Regardless of upload method, the custom layout will be saved internally and thus only needs to be loaded once.

## Picotool Upload

Direct uploads are a two step process.

* Create and download your custom mapping using the [Pico2Maple Controller Mapper](https://cluoma.github.io/Pico2Maple-config/) webpage.
* Upload the mapping to your Pico2Maple using `picotool`.

Creating and download a mapping is fairly straightforward using the [Mapper webpage](https://cluoma.github.io/Pico2Maple-config/). Be sure to use the 'Download Mapping for Picotool Upload' button.

Once downloaded, connect Pico2Maple in BOOTSEL mode (connect to a computer while holding down the BOOTSEL button), and execute the following `picotool` command: `picotool load "pico2maple-mapping.bin" -o 0x103FC000`.

## SD Card Upload

Loading a custom controller layout using an SD card is also fairly straightforward.

Configure your layout using the [Pico2Maple Controller Mapper](https://cluoma.github.io/Pico2Maple-config/) webpage and download it using the 'Download Mapping for microSD Card' button.

Copy the downloaded file to the `/pico2maple/` folder on your SD card.

## The Config File

The following section describes the full details the controller map config file that is used for loading to an SD card.

For the adventurous folks, editting this file directly may be simpler than using the webpage.

### File Location

Pico2Maple will attempt to parse a controller layout from a file named `pico2maple_controller_map.cfg` placed in the `/pico2maple/` directory of the SD card.

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

### Limitations

* Any input can be mapped to any output.
* Up to 4 inputs can be mapped to same output. E.g. `RB` and `LB` could both map to `B`.
    * When multiple inputs map to the same output, the value of the output is determined in an OR fashion. E.g. `B` will be pressed if either `RB` *OR* `LB` is pressed.
* The same input may be mapped to multiple outputs. E.g. `DPAD_UP` could activate both `A1_UP` *and* `DPAD_UP`.
* Analog axis for LEFT/RIGHT and UP/DOWN will cancel each other out if both are activated.

Any custom mapping targeting a non-standard Dreamcast button - such as `C`, `Z`, the second analog etc. - will cause Pico2Maple to report itself to the Dreamcast as a controller that has all these buttons. Some games do not like this (e.g. *Evolution 2*) and will refuse to recognize the controller. A custom mapping that only targets buttons on a standard Dreamcast controller will cause Pico2Maple to show up as a standard controller to the Dreamcast and will avoid this issue.

### Options

Options in remapping files follow the same format as buttons, e.g. `OPTION_AUTOLOAD: TRUE`.

#### Autoload

`OPTION_AUTOLOAD: FALSE/TRUE`

This option tells Pico2Maple whether or not this layout should be loaded automatically.
