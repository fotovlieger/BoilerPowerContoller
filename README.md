# BoilerPowerContoller
220V power controller that diverts excess solar power to an electric water boiler. Controller is interfaced to HomeAssistant

## Harware
- A simple electric boiler (no electronics, just a heating element and 'mechanical' thermostat)
- A cheap [thyristor voltage regulator](voltageregulator.md) with display and buttons
- Esp32 microcontroller
- temperature sensor to monitor water temperature

Note: the 'ground' ans signals to/from the power controler are connected to the 220V mains! Optocouplers an a power source for the esp32 are needed. (to be able to connect to its usp port while running or connect external (grounded) sensors)

## Software setup

- Main idea is to control the thyristor circuit by generating trigger pulses. Controlling the deleay of these pulses
  relative to the 50Hz zero crossing allows to control the output power to the boiler.
- Must be in C++: latency of micropython on esp32 is not good enough (must be better that 1ms, preferably 100us)
- interface to HASS: direct or via MQTT
- Implementation: based on EspHome, external component (replaces legacy 'custom component')
