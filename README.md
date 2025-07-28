
See our [Releases](https://github.com/HandHeldLegend/SInput-HID/releases)

# What is SInput?

SInput is a targetable HID setup that device makers may utilize to enable better native compatibility with SDL.


You may use USB Device ID *0x10C6* along with Vendor ID *0x2E8A* if you wish to use the fallback mapping and have a generic input function within SDL. Please note that this is better for device testing only. If you wish to have native mapping support, it is better to register your own USB PID.

If you have further questions about native SDL implementation or extension, [join our Discord channel to discuss SInput](https://discord.gg/Rh8cnS7wJA)

## Documentation
All current [documentation is available on our wiki](https://docs.handheldlegend.com/s/sinput).


## Supported Devices List

| Device | Maker | URL |
|----|----|----|
| GC Ultimate | Hand Held Legend, LLC. | [https://gcultimate.com]() |
| ProGCC | Hand Held Legend, LLC. | [Product Page](https://handheldlegend.com/products/progcc-kit-wireless-wired-bundle) |
| Super Gamepad+ | Hand Held Legend, LLC. | [Product Page](https://docs.handheldlegend.com/s/portal/doc/super-gamepad-MiOt0KLuX4) |
| Firebird (Pending) | Bonjiri Channel | [Product Page](https://booth.pm/ja/items/4934916) |


## Features

| Feature | Notes |
|----|----|
| Digital Buttons | Support for *up to* 32 buttons |
| Gyro | 3 axis gyro |
| Accelerometer | 3 axis accelerometer |
| Fast Polling | 1khz polling rates |
| Haptics | Stereo haptics |
| Player LED | Indicate which player your gamepad is registered as |
| Touchpad Support | Support for 2 touchpad inputs |
