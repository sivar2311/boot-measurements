# Description
Runtime measurements of a SinricPro sketch on an ESP32 (Firebeetle32 board).

The sketch connects to the SinricPro server and sends a temperature event with random values for temperature and humidity. After sending, the connection is disconnected and the ESP32 goes into deep-sleep mode. After a defined time, the ESP32 wakes up from deep-sleep and repeats this process.

# Measurements
| # | SSL | D/S | WIFI-CACHE | boot-loader | flash-mode | flash speed | boot | deep-sleep |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|-:|
|1| yes|D|no|standard|DIO|40Mhz| [3900 ms](./png/01a.png) | [3720 ms](./png/01b.png)
|2| no|D|no|standard|DIO|40Mhz|  [3030 ms](./png/02a.png) | [3010 ms](./png/02b.png)
|3| no|D|yes|standard|DIO|40Mhz| [3040 ms](./png/03a.png) | [1270 ms](./png/03b.png) 
|4| no|S|yes|standard|DIO|40Mhz| [2760 ms](./png/04a.png) | [1080 ms](./png/04b.png)
|5| no|S|yes|optimized|DIO|40Mhz|[2770 ms](./png/05a.png) | [ 720 ms](./png/05b.png)
|6| no|S|yes|optimized|QIO|40Mhz|[2700 ms](./png/06a.png) | [ 710 ms](./png/06b.png)
|7| no|S|yes|optimized|QIO|80Mhz|[2640 ms](./png/07a.png) | [ 680 ms](./png/07b.png)

Click on the time to see the corresponding oscillogram.
## Legend

### SSL
- yes: SinricPro connection using SSL (default)
- no: SinricPro connection not using SSL (`#define SINRICPRO_NOSSL`)

### D/S
- D: WiFi DHCP configuration
- S: WiFi static-ip configuration

### WIFI-CACHE
1st-boot is performed as usual. When the wifi connection has been established the wifi-channel and the bssid are cached for later reuse.
Wake-up from deep sleep connect to the wifi with cached values from 1st-boot

### boot-loader
- standard: Standard Arduino Espressif32 bootloader
- optimized:
  - no serial debug output
  - no flash validation when wakeup from deep-sleep

### boot / deep-sleep
Measurements during normal start-up / waking up from deep-sleep