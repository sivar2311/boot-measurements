# Description
Runtime measurements of a SinricPro sketch on an ESP32 (Firebeetle32 board).

The sketch connects to the SinricPro server and sends a temperature event with random values for temperature and humidity. After sending, the connection is disconnected and the ESP32 goes into deep-sleep mode. After a defined time, the ESP32 wakes up from deep-sleep and repeats this process.

# Measurements
| # | boot-type | SSL | D/S | WIFI-CACHE | boot-loader | flash-mode | flash speed | time |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|-:|
|1a| 1st boot |yes|D|no|standard|DIO|40Mhz| [3900 ms](./png/01a.png) |
|1b| wake-up |yes|D|no|standard|DIO|40Mhz|  [3720 ms](./png/01b.png) |
|2a| 1st boot |no|D|no|standard|DIO|40Mhz|  [3030 ms](./png/02a.png) |
|2b| wake-up |no|D|no|standard|DIO|40Mhz|   [3010 ms](./png/02b.png) |
|3a| 1st boot |no|D|yes|standard|DIO|40Mhz| [3040 ms](./png/03a.png) |
|3b| wake-up |no|D|yes|standard|DIO|40Mhz|  [1270 ms](./png/03b.png) |
|4a| 1st boot |no|S|yes|standard|DIO|40Mhz| [2760 ms](./png/04a.png) |
|4b| wake-up |no|S|yes|standard|DIO|40Mhz|  [1080 ms](./png/04b.png) |
|5a| 1st boot |no|S|yes|optimized|DIO|40Mhz|[2770 ms](./png/05a.png) |
|5b| wake-up |no|S|yes|optimized|DIO|40Mhz| [ 720 ms](./png/05b.png) |
|6a| 1st boot |no|S|yes|optimized|QIO|40Mhz|[2700 ms](./png/06a.png) |
|6b| wake-up |no|S|yes|optimized|QIO|40Mhz| [ 710 ms](./png/06b.png) |
|7a| 1st boot |no|S|yes|optimized|QIO|80Mhz|[2640 ms](./png/07a.png) |
|7b| wake-up |no|S|yes|optimized|QIO|80Mhz| [ 680 ms](./png/07b.png) |

Click on the time to see the corresponding oscillogram.
## Legend

### boot-type:
- 1st-boot (normal)
- wake-up (wakeup from deep-sleep)

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