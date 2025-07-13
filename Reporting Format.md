# Input Report 0x01 (64 bytes)

Our input reports also contain command response data if necessary.

## C Struct Definition

Note that this format is not portable. LSB is indicated here for posterity. Implement at your own discretion.

```clike
#pragma pack(push, 1) // Ensure byte alignment
// Input report (Report ID: 1)
typedef struct
{
    uint8_t plug_status;    // Plug Status Format
    uint8_t charge_percent; // 0-100

    union {
        struct {
            uint8_t button_a   : 1; // LSB
            uint8_t button_b   : 1;
            uint8_t button_x   : 1;
            uint8_t button_y   : 1;
            uint8_t dpad_up    : 1;
            uint8_t dpad_down  : 1;
            uint8_t dpad_left  : 1;
            uint8_t dpad_right : 1;
        };
        uint8_t buttons_1;
    };

    union
    {
        struct
        {
            uint8_t button_stick_left : 1; // LSB
            uint8_t button_stick_right : 1;
            uint8_t button_l_shoulder : 1;
            uint8_t button_r_shoulder : 1;
            uint8_t button_l_trigger : 1;
            uint8_t button_r_trigger : 1;
            uint8_t button_l_paddle_1 : 1;
            uint8_t button_r_paddle_1 : 1;
        };
        uint8_t buttons_2;
    };

    union
    {
        struct
        {
            uint8_t button_start  : 1; // LSB
            uint8_t button_select : 1;
            uint8_t button_guide  : 1;
            uint8_t button_share  : 1;
            uint8_t button_l_paddle_2 : 1;
            uint8_t button_r_paddle_2 : 1;
            uint8_t button_l_touchpad : 1;
            uint8_t button_r_touchpad : 1;
        };
        uint8_t buttons_3;
    };

    union
    {
        struct
        {
            uint8_t button_power   : 1; // LSB
            uint8_t button_misc_4  : 1;
            uint8_t button_misc_5  : 1;
            uint8_t button_misc_6  : 1;
            
            // Misc 7 through 10 is unused by
            // SDL currently!
            uint8_t button_misc_7  : 1; 
            uint8_t button_misc_8  : 1;
            uint8_t button_misc_9  : 1;
            uint8_t button_misc_10 : 1;
        };
        uint8_t buttons_4;
    };

    int16_t left_x;             // Left stick X
    int16_t left_y;             // Left stick Y
    int16_t right_x;            // Right stick X
    int16_t right_y;            // Right stick Y
    int16_t trigger_l;          // Left trigger
    int16_t trigger_r;          // Right trigger
    uint16_t gyro_elapsed_time; // Microseconds, 0 if unchanged
    int16_t accel_x;            // Accelerometer X
    int16_t accel_y;            // Accelerometer Y
    int16_t accel_z;            // Accelerometer Z
    int16_t gyro_x;             // Gyroscope X
    int16_t gyro_y;             // Gyroscope Y
    int16_t gyro_z;             // Gyroscope Z

    int16_t touchpad_1_x;       // Touchpad/trackpad
    int16_t touchpad_1_y;
    int16_t touchpad_1_pressure;

    int16_t touchpad_2_x;
    int16_t touchpad_2_y;
    int16_t touchpad_2_pressure;

    uint8_t reserved_bulk[19];  // Reserved for command data
} sinput_input_s;
#pragma pack(pop)
```

## Data Table

| Byte | Data | Type | Notes |
|----|----|----|----|
| 0 | Report ID | uint8 | 0x01 |
| 1 | Plug Status | uint8 | [Plug Status Format](Plug%20Status%20Format.md)  |
| 2 | Charge Percent | uint8 | 0-100 |
| 3-6 | Buttons | uint8\[4\] | [Buttons Format](Buttons%20Format.md)  |
| 7-8 | Left X | int16 | INT 0 is center |
| 9-10 | Left Y | int16 | INT 0 is center |
| 11-12 | Right X | int16 | INT 0 is center |
| 13-14 | Right Y | int16 | INT 0 is center |
| 15-16 | Trigger L | int16 | INT16_MIN to INT16_MAX |
| 17-18 | Trigger R | int16 | INT16_MIN to INT16_MAX |
| 19-20 | Gyro Elapsed Time | uint16 | Microseconds. 0 if unchanged (repeat data) |
| 21-22 | Accel X (Gs) | int16 | 0 is neutral |
| 23-24 | Accel Y | int16 | 0 is neutral |
| 25-26 | Accel Z | int16 | 0 is neutral |
| 27-28 | Gyro X (DPS) | int16 | 0 is neutral |
| 29-30 | Gyro Y | int16 | 0 is neutral |
| 31-32 | Gyro Z | int16 | 0 is neutral |
| 33-34 | Touch 1 X | int16 |    |
| 35-36 | Touch 1 Y  | int16 |    |
| 37-38 | Touch 1 Pressure | uint16 |    |
| 39-40 | Touch 2 X  | int16 |    |
| 41-42 | Touch 2 Y | int16 |    |
| 43-44 | Touch 2 Pressure | uint16 |    |
| 45-63 | Reserved |    |    |


# Input Report 0x02 (64 bytes)

Input report 2 contains command response data

| Byte | Data | Notes |
|----|----|----|
| 0 | 0x03 | REPORT ID |
| 1 | Various | COMMAND ID |
| 2-63 | Various | COMMAND DATA |


# Output Report 0x03 (48 bytes)

Output report 3 contains 48 bytes and command data.

| Byte | Data | Notes |
|----|----|----|
| 0 | 0x02 | REPORT ID |
| 1 | Various | COMMAND ID |
| 2-47 | Various | COMMAND DATA |

## Command 0x01 - Haptics


No acknowledgement is sent to the host for this command

### C Struct Definition

```clike
#pragma pack(push, 1) // Ensure byte alignment

typedef struct 
{
    uint8_t type;

    union 
    {
        // Frequency Amplitude pairs
        struct 
        {
            struct
            {
                uint16_t frequency_1;
                uint16_t amplitude_1;
                uint16_t frequency_2;
                uint16_t amplitude_2;
            } left;

            struct
            {
                uint16_t frequency_1;
                uint16_t amplitude_1;
                uint16_t frequency_2;
                uint16_t amplitude_2;
            } right;
            
        } type_1;

        // Basic ERM simulation model
        struct 
        {
            struct 
            {
                uint8_t amplitude;
                bool    brake;
            } left;

            struct 
            {
                uint8_t amplitude;
                bool    brake;
            } right;
            
        } type_2; 
    };
} sinput_haptic_s;

#pragma pack(pop)
```

### Haptics Type 1 - Precise Stereo Haptics

The haptic data is comprised of a frequency/amplitude pair. 

The target driving frequency range is **40hz to 2000Hz.**

| Byte | Data | Type | Value |
|----|----|----|----|
| 0 | Command | uint8 | 0x01 |
| 1 | Type | uint8 | 0x01 |
| 2-3 | Frequency 1 Left | uint16 |    |
| 4-5 | Amplitude 1 Left | uint16 |    |
| 6-7 | Frequency 2 Left | uint16 |    |
| 8-9 | Amplitude 2 Left | uint16 |    |
| 2-3 | Frequency 1 Right | uint16 |    |
| 4-5 | Amplitude 1 Right | uint16 |    |
| 6-7 | Frequency 2 Right | uint16 |    |
| 8-9 | Amplitude 2 Right | uint16 |    |


### Haptics Type 2 - ERM Stereo Haptics

This is simply an 8 bit amplitude, and a bool brake value

| Byte | Data | Type | Value |
|----|----|----|----|
| 0 | Command | uint8 | 0x01 |
| 1 | Type | uint8 | 0x02 |
| 2 | Amplitude Left | uint8 |    |
| 3 | Brake Left | bool |    |
| 4 | Amplitude Right | uint8 |    |
| 5 | Brake Right | bool |    |


## Command 0x02 - Features Request

This command is sent from SDL to retrieve features associated with SDL.

**The device must acknowledge this command to be initialized by SDL.**


### Command Response

| Byte | Data | Meaning |
|----|----|----|
| 0 | Various | Feature Flags 1 ( See [Feature Flags Format](Features%20Response%20Bytes.md) ) |
| 1 | Various | Feature Flags 2 ( See [Feature Flags Format](Features%20Response%20Bytes.md) ) |
| 2 | 0x00-0xFF | SDL Gamepad Type |
| 3 | 0x00-0xFF | SDL Gamepad SubType |
| 4 | 0x00 | Sensor polling rate (milliseconds) |
| 5 | 0x00 | Reserved |
| 6-7 | Uint16 | Accelerometer G force range |
| 8-9 | Uint16 | Gyroscope DPS sensitivity range |
| 10-13 | Uint8 | Button Usage Masks ( See [Buttons Format](Buttons%20Format.md) ) |
| 14 | Uint8 | Touchpad Count (**Max 2 touchpads**) |
| 15 | Uint8  | Touchpad Finger Count (**Max 2 fingers TOTAL**) |



## Command 0x03 - Set Player LEDS

No acknowledgement is sent to the host for this command

Send a byte of 0x00 up to 0xFF for player number.


## Command 0x04 - Set Joystick RGB LED

No acknowledgement is sent to the host for this command

Sends 3 bytes representing a 24 bit RGB value for the gamepad to display whichever way it chooses. Byte order is red, green, blue.