# pedal-actions

Script that grabs a HID foot pedal and translates the key presses into actions.

For most Foot Pedal devices, special Windows software is required to set the mapping.
The idea of this script is: Configure the Foot Pedal once, then use evdev and uinput to
re-map the actions as needed.

As the first argument, pass the path to one of the input devices in `/dev/input/by-id`.
That input device will be grabbed completely.
This can be dangerous: Accidentally grabbing the wrong keyboard means that you can
no longer control your computer - even hotkeys like Ctrl+Alt+F1 will no longer work!

For each foot pedal, pass a `--key` flag, followed by the name of the key that is
bound to the pedal and the actions that should be performed when the pedal is pressed.

Example:

`./pedal_actions /dev/input/by-id/usb-MKEYBOARD_3011-event-kbd --key A notify print`

Available actions:

- `notify`
  Send libnotify notifications when pedals are pressed and released
- `print`
  Print to stdout when pedals are pressed and released
- `quit`
  Quit when the pedal is pressed
- `key:{key name}`
  Simulate a key press. When the pedal is pressed, the key is pressed.
  When the pedal is released, the key is released.
- `mouse:{color code}`
  Shows a translucent window with a crosshair with the given color code
  (6 hex digits) in it.
  Move the crosshair to the pixel that should be clicked.
  When the pedal is pressed, the mouse is moved to the center of the
  crosshair and a click is simulated.
- `script:{path}`
  When the pedal is pressed, the script is executed.

Full example:

`./pedal_actions /dev/input/by-id/usb-MKEYBOARD_3011-event-kbd --key A key:leftshift --key B mouse:ff0000`
