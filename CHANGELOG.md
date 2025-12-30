# Pico2Maple Changelog

## 2025-12-29

* Support pairing and use of some BT keyboards (only one has been tested)
* Add support for SJ@JX arcade stick USB board
* Improve maple timings

## 2025-11-15

* Improved Switch Pro controller support on USB and BT

## 2025-10-24

* Added rumble support for PS4, PS5, and Xbox controllers on USB and BT. Select + Dpad Down to enable/disable.

## 2025-10-04

* Improved deadzone handling of analog sticks for all XInput devices using USB

## 2025-09-25

* Fixed bug in custom mappings where left and right bumpers were ignored
* Added text mapping download to [Pico2Maple Mapper tool](https://cluoma.github.io/Pico2Maple-config/) for easy SD card loading

## 2025-09-07

* Added a new layout which will appear as an official Dreamcast Racing Wheel to games that support it. Press Select + Dpad Left to enable.
* Added support for Logitech G29 Racing Wheel via USB with PS4 mode. Have a racing wheel you want supported? Make a GitHub issue or join the Discord server to discuss!

## 2025-08-01

* Fully tested USB and BT support for PlayStation 4 controller. Many third-party PS4 compatible controllers will be detected but are untested.
* Move to pico-sdk 2.2.0

## 2025-07-17

* Fully tested USB support for PlayStation 3 controller. Many third-party PS3 compatible controllers will be detected but are untested. GP-2040CE now works with either PS3 or XInput modes.
* Improved Twin Stick controller mapping to accommodate Hori 360 Twin Sticks.
* BT support for Dreamwave controller.

## 2025-06-14

* Experimental support for custom controller layouts/remapping, an SD card is required to load the layout. More info at [CONTROLLER_LAYOUTS.md](CONTROLLER_LAYOUTS.md).

## 2025-05-18

* Added a Fight Stick layout to accommodate typical stick layouts where the fifth and sixth buttons are RB and RT. Press Select + Y to enable. This layout remaps RB and RT inputs to the Z and C buttons on the Dreamcast respectively.

## 2025-05-13

* Implemented HID report parsing for handling a wider range of USB devices. PS3/4 controllers *may* work, give it a try
* Much improved USB mouse compatibility with proper HID parsing
* Small improvements to controller input handling

## 2025-04-09

* Wireless support for Pico2 W boards. A USB device will be used if detected, otherwise will search for a bt device.
* Refactoring of USB code

## 2025-03-03

* Add support for Twin Stick layout, press Select+X to enable
* OLED improvements
* Change VMU data location on flash storage, backup your internal VMU data before updating
* Automatically backup internal VMU data to microSD card on boot
* Additional stability improvements in preparation for bluetooth support

## 2025-02-09

* Improved stability of the Maple bus
* Additional OLED display features showing what type of device is active (controller, keyboard, or mouse)

## 2024-12-15

* Initial release