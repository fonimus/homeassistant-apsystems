# APsystems Sensor for Home Assistant
This component simplifies the integration of a APsystems inverter:
* creates up to individuals sensors for easy display or use in automations
* collects power (W) and energy (KWH) every 5 minutes. There is also a sensor for daily total and max power.
* extract data from apsystemsema.com web portal instead of hack the ECU connection
* supports any kind of ASsystems inverter or ECU
* if enabled, pauses from sunset to sunrise (basically when there no sun)
* have a cache system to avoid individual sensors request the same data to apsystemsema.com. It is a great feature for I/O (HTTP) performance.
* there is a date sensor to identify exactly date/time refers each sensor data

### URL's Utilised
The URL called is ``https://www.apsystemsema.com/ema/ajax/getDashboardApiAjax/getDashboardProductionInfoAjax``
It is only called from sunset to sunrise and the sensor going offline at night

### Installation
Use [HACS](https://custom-components.github.io/hacs/) to point to this github URL: https://github.com/fonimus/homeassistant-apsystems

### Configuration
Use your apsystemsema.com to configure the configuration.yaml.

```yaml
# Minimal configuration.yaml entry:
sensor:
  - platform: apsystems
    authId: apsystemsem_authid
    systemId: apsystemsema_system_id
    ecuId: apsystemsema_ecu_id
    sunset: off
```
1 - set "Allow visitors to access to this system" and get the authid from here

2 - your systemId is found at apsystemsema.com. See the page source code and at the Settings Menu there is a code like that:
```html
<span>Settings</span>
<ul>
    <li onclick="managementClickCustomer('YOUR SYSTEM ID')"><a>Settings</a></li>
    <li onclick="intoFaq(10)"><a>Help</a></li>
</ul>
```
Get the system id inside the ```managementClickCustomer()```.

3 - There is an ecu id data at https://apsystemsema.com/ema/security/optmainmenu/intoLargeReport.action

4 - sunset attribute could be on or off

### Debug
To get debug info in the logs do
```yaml
logger:
  default: info
  logs:
    custom_components.apsystems: debug
```

and then grep the log for output

```bash
grep apsystem home-assistant.log
```
