# Feature Flags Handshake
It’s highly recommended, but not required, that you respond to the command for feature flags request.

This allows you to report to SDL what the sensitivity of your sensors are to ensure a consistent gameplay experience with motion controls.


# Handshake Process

## Gamepad Connected

When the gamepad is connected to an HID service, SDL will pick up that this device is connected, and it will attempt to check if the VID/PID matches. If it matches one of the valid VID/PID for SInput, it will load the appropriate driver.


## Driver Loading

When the SDL driver is loaded for SInput, it will send an Output report with the command to request the feature report data. (See [Report Formats](Reporting%20Format.md)


The Gamepad is expected to respond to this format when being used with SDL. SDL needs information such as the button count and a button usage mask so the driver knows how to apply button inputs appropriately.


## Player LED Setting

When the SDL driver receives the feature flag command response data, it will initialize the controller and finally issue a command to allow your gamepad to be aware of its player number. 

