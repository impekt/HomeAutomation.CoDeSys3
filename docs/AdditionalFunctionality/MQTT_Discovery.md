## **MQTT discovery**

Several home automation systems -like Home Assistant- support [MQTT discovery](https://www.home-assistant.io/integrations/mqtt/#mqtt-discovery). Leveraging this functionality in the PLC programming will automatically provision devices in the supported home automation system.

----------------------------

:information_source: Function blocks supporting MQTT discovery are marked with a ![MQTT Discovery](https://img.shields.io/badge/MQTT%20Discovery-brightgreen) badge on their documentation page.

----------------------------

Supported function blocks have a `InitMqttDiscovery` method. The method needs a [FB_HomeAssistant_DEVICE](../FunctionBlocks/FB_HomeAssistant_DEVICE.md) instance to work.

- InitMqttDiscovery: Sets all config needed for letting Home Assistant discover the entity automatically.
  - `name`: The name show in Home Assistant frond-end
  - `MqttDiscoverPrefix`: Pointer to string prefix for the MQTT discover topic
  - `Device`: The device show in Home Assistant
  - `overruleId`: OPTIONAL. Leave empty to set it to the device + instance name HOUSE_FB_AO_DIMMER_001 for instance name, or overule to e.g. MY_DIMMER_GND_HALL_01
  - `icon`: OPTIONAL. Specify icon. Default changes per function block
  - `meta`: OPTIONAL. Free field for meta data. Only visible in MQTT

Example:

```ST
FB_AO_DIMMER_001.InitMqttDiscovery(
	name := 'Office strip cold',                        (* The name show in Home Assistant frond-end*)
	overruleId:= 'Dimm_office_cw',                      (*  e.g. 'MY_DIMMER_GND_HALL_01'  *)
	icon := 'mdi:lightbulb',                            (* specify icon*)
	MqttHADiscoveryPrefix:= ADR(MqttHADiscoveryPrefix), (* pointer to string prefix for the MQTT discover topic *)
	Device := FB_HomeAssistant_DEVICE,						      (* The device show in Home Assistant *)
	meta := 'GeoDev office',								            (* Free field for meta data. Only visible in MQTT *)
);
```