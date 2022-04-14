# Home Assistant Custom Component - Generic Water Heater

The `Generic Water Heater` water_heater platform is a Water Heater implemented in Home Assistant. It uses a sensor and a switch connected to a domestic hot water (DHW) reservoir and a heat source (eg. resistance). When "on", if the measured temperature is cooler than the target temperature, the heater will be turned on, and turned off when the required temperature is reached. 

```yaml
# Example configuration.yaml entry
generic_water_heater:
  bath water:
    heater_switch: switch.dhw_switch
    temperature_sensor: sensor.dhw_temperature
    target_temperature: 50
    delta_temperature: 5
```

## Installation 

Manual

- Place the custom_components folder in your configuration directory (or add its contents to an existing custom_components folder). It should look similar to this:

```
<config directory>/
|-- custom_components/
|   |-- generic_water_heater/
|       |-- __init__.py
|       |-- water_heater.py
```

- Edit your configuration.yaml file according to the example above

## HACS

If you want HACS to handle installation and updates, add _Generic Water Heater_ as a custom repository. In this case, it is recommended that you turn off automatic updates, as above. 

## Configuration
| Option | Required | Type | Description |
--- | --- | --- |--- 
heater_switch | True | string | `entity_id` for heater switch, must be a toggle device.
temperature_sensor | True | string | `entity_id` for a temperature sensor, temperature_sensor.state must be temperature.
target_temperature | False | float | Set initial target temperature. Failure to set this variable will result in target temperature being set to null on startup
delta_temperature | False | float | In order to avoid continuous on/off triggering of the heater a delta_temperature can be defined, where by the heater turns off below the `target_temperature` minus the `delta_temperature`.

Currently the `Generic Water Heater` climate platform supports 'on' and 'off' modes. 

The `Generic Water Heater` has a failsafe mechanism by which if the temperature sensor becomes unavailable the heater is turned off.

