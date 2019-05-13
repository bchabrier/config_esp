# config_esp
A configuration manager for [esp_wifi_repeater](https://github.com/martin-ger/esp_wifi_repeater).

This is a simple configuration manager for ESP devices installed as WiFi repeaters running [esp_wifi_repeater](https://github.com/martin-ger/esp_wifi_repeater). Among others, it allows to display, edit and upload the configuration of the devices, including GPIO settings. It is also possible to display the topology, or to connect to each device with a command line interface. In addition, you can upload a new firmware to a single device, or to all devices in one shot.


## Installation
`config_esp` is a simple shell script that does not need any installation *per se* - simply copy the file and set it as executable. However, it communicates with the ESP WiFi repeaters through an MQTT server, hence it needs [mosquitto](https://mosquitto.org/) to be installed, and the ESP devices to be initially set up with the proper host, user and password with `set mqtt_host`, `set mqtt_user` and `set mqtt_password`.

`config_esp` stores the configuration in `~/.config_esp.conf`.

## Sample usage

### Main menu

```
$ ./config_esp
What action?
1) Show config
2) Show GPIO config
3) Upload config
4) Upload firmware
5) Enter command line
6) Display graph
7) Edit config file
8) Quit
Enter action (1-8) [1]: 2
Select an ESP:
1) ESP_04a87b - Filtration piscine
2) ESP_04a92c - Wemos D1 Mini du garage
3) ESP_9c4c90 - Grand Portail
all) All ESPs
Enter ESP number (1-3|all):
```

### Show config

```
ESP_04a92c - Wemos D1 Mini du garage
------------------------------------
> show config
Version V2.2.9 (build: Sun May 12 11:26:38 2019)
STA: SSID:Wifi_Home PW:lamerestbleue
BSSID: 24:24:01:2c:49:77
Automesh: on (operational) Level: 2 Threshold: -85
AP:  SSID:Wifi_Home_ESP  PW:XXXXXXXXX IP:10.24.2.1/24 [NAT]
STA MAC: 38:2b:78:04:a9:2c
AP MAC:  24:24:02:3d:ad:cf
STA hostname: ESP_04a92c
Network console access on port 7777 (mode 3)
Clock speed: 80
MQTT: enabled
```
### Show GPIO config
```
ESP_9c4c90 - Grand Portail
--------------------------
> show gpio
GPIO 4: in_pullup, triggers GPIO 12 as a bistable normally open
GPIO 5: in_pullup, triggers GPIO 14 as a bistable normally open
GPIO 12: out
GPIO 13: out
GPIO 14: out
GPIO 15: out
```

### Enter command line
```
ESP_04a87b - Filtration piscine
-------------------------------
Entering in command line mode with ESP_04a87b. Type 'quit' to end the session...
CMD> show config
Version V2.2.9 (build: Sun May 12 11:26:38 2019)
STA: SSID:Wifi_Home PW:XXXXXXX
BSSID: a0:40:a0:99:cc:a7
Automesh: on (operational) Level: 1 Threshold: -85
AP:  SSID:Wifi_Home_ESP  PW:XXXXXX IP:10.24.1.1/24 [NAT]
STA MAC: 38:2b:78:04:a8:7b
AP MAC:  24:24:01:4f:b5:57
STA hostname: ESP_04a87b
Network console access on port 7777 (mode 3)
Clock speed: 80
MQTT: enabled

CMD>
```
### Display topology

```
SSID: Wifi_Home
a0:40:a0:99:cc:a7
||
|+--ESP_04a87b: Filtration piscine
|   AP SSID: Wifi_Home_ESP - 38:2b:78:04:a8:7b - 192.168.0.50
|   Version V2.2.9 (build: Sun May 12 11:26:38 2019)
|   Uptime: 1d 04:49:13, 14 KiB in (62 packets), 4 KiB out (10 packets)
|   Signal strength: 28% (-86 dBm), Free mem: 10840, Power supply: 2.966V, Clock: 80 MHz
|   No station connected
|
+--ESP_9c4c90: Grand Portail
   AP SSID: Wifi_Home_ESP - 5c:cf:7f:9c:4c:90 - 192.168.0.51
   Version V2.2.9 (build: Sun May 12 11:26:38 2019)
   Uptime: 1d 01:48:07, 13950 KiB in (87894 packets), 37705 KiB out (96663 packets)
   Signal strength: 64% (-68 dBm), Free mem: 8912, Power supply: 2.909V, Clock: 80 MHz
   2 stations connected
   |
   +--ESP_04a92c: Wemos D1 Mini du garage
      AP SSID: Wifi_Home_ESP - 38:2b:78:04:a9:2c - 10.24.1.2
      Version V2.2.9 (build: Sun May 12 11:26:38 2019)
      Uptime: 14:50:59, 0 KiB in (0 packets), 0 KiB out (0 packets)
      Signal strength: 52% (-74 dBm), Free mem: 11040, Power supply: 2.983V, Clock: 80 MHz
      No station connected
Press a key to stop...
```

