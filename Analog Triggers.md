Analog triggers are the primary L and R option on Xbox gamepads and more. Not all gamepads may have analog triggers, so there are a few recommended methods of handling analog triggers listed below.

# Simple Analog Triggers

Analog triggers may be sent using the trigger_l and trigger_r fields as a signed 16 bit value as normal.


# Digital Only Triggers

Triggers may be sent using the digital button_l_trigger and button_r trigger fields. SDL will automatically recognize these and apply a full analog value.


# Dual Stage Analog Triggers

For triggers that support analog values, with a digital press, assign the digital press to the button_l_paddle_1 and button_r_paddle_1 fields.

Send the analog trigger values to trigger_l and trigger_r fields.