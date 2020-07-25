# Outdoor Pir sensor with ESP8266

use the following code:

```yaml
wifi_ssid: "your_ssid"
wifi_password: "your_passwd"
ota_passwd: "ota_passwd"
api_passwd: "api_passwd"
```

```yaml
substitutions:
  plug_name: pir4
  locatie: poortachtertuin
  <<: !include .substitutions.yaml

esphome:
  name: ${plug_name}
  platform: ESP8266
  board: d1_mini

wifi:
  ssid: ${wifi_ssid}
  password: ${wifi_password}
  manual_ip:
    static_ip: 192.168.2.195
    gateway: 192.168.2.254
    subnet: 255.255.255.0

ota:
  password: ${ota_passwd}

api:
  password: ${api_passwd}

web_server:
  port: 80

# Enable logging
logger:

time:
  - platform: homeassistant
    id: homeassistant_time

binary_sensor:
  - platform: gpio
    pin:
      number: D1
      inverted: true
    id: ${plug_name}
    name: "${plug_name}  ${locatie}"
    device_class: motion
```
