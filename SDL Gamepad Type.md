
This type does not necessarily map to first-party controllers from Microsoft/Sony/Nintendo; in many cases, third-party controllers can report as these, either because they were designed for a specific console, or they simply most closely match that console's controllers (does it have A/B/X/Y buttons or X/O/Square/Triangle? Does it have a touchpad? etc). 

| Gamepad Type | Value |
|----|----|
| Unknown | 0 |
| Standard | 1 |
| Xbox 360 | 2 |
| Xbox One | 3 |
| PS3 | 4 |
| PS4 | 5 |
| PS5 | 6 |
| Nintendo Switch Pro | 7 |
| Nintendo Joy-Con Left | 8 |
| Nintendo Joy-Con Right | 9 |
| Nintendo Joy-Con Pair | 10 |
| Nintendo GameCube  | 11 |


# Sub-Type

The 4 most significant bits resolve to a specific face style in SDL where 1 = ABXY and so on according to the below enum definition from SDL.

```clike
typedef enum
{
    SDL_GAMEPAD_FACE_STYLE_UNKNOWN,
    SDL_GAMEPAD_FACE_STYLE_ABXY,
    SDL_GAMEPAD_FACE_STYLE_AXBY,
    SDL_GAMEPAD_FACE_STYLE_BAYX,
    SDL_GAMEPAD_FACE_STYLE_SONY,
} SDL_GamepadFaceStyle;
```


The 4 least significant bits can be used to distinguish different devices that share a PID/VID and have a unique mapping. This basically serves to create community mappings. Devices having a unique name will also alter the GUID allowing for community maps to exist alongside other devices.