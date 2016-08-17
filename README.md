# get_all_apps.sh
This script allows on downloading all known *Mi Fit* APK from *apkmirror.com*.
After download, each APK is unzipping and all firmwares (i.e Mili.fw, running.fw) is copied to `./fw/VERSION/`

### needs
* [xidel](http://www.videlibri.de/xidel.html)

### usage
./get_all_apps.sh [-f | -u ]

```
-u|--unzip - auto-unzip each APK and copy FW to separate directory"
-f|--force - Download APK even when corresponding file for this version already exist"
```

# parse_fw
Simple script (escript) writted in Erlang. Allow extract firmware version from Mili.hr

### needs
```bash
apt-get install erlang
```
or use [kerl](https://github.com/yrashk/kerl)

### usage
```bash
$ ./parse_fw fw/1.8.711/Mili.fw
#{crc32 => "F6662DE3",file_name => "Mili.fw",version => {1,0,12,0}}
```

# Version firmwares in APKs

| APK Version | Mili.fw | CRC32 | Mili_hr.fw | CRC32 | running.fw | CRC32 | weight.fw | CRC32 |
|-------------|---------|-------|------------|-------|------------|-------|-----------|-------|
| 1.3.412 | 1.0.9.14 | 2AA422D3 | - | - | - | - | ? |
| 1.4.452 | 1.0.9.48 | 9A648EB8 | - | - | - | - | ? |
| 1.4.614 | 1.0.9.55 | 6939E682 | - | - | - | - | ? |
| 1.4.641 | 1.0.9.48 | 9A648EB8 | - | - | - | - | ? |
| 1.4.923 | 1.0.9.65 | 132AC14C | - | - | - | - | ? |
| 1.4.924 | 1.0.9.65 | 132AC14C | - | - | - | - | ? |
| 1.5.331 | 1.0.9.79 | BFF50CBC | 4.15.5.14 | D486E623 | - | - | ? |
| 1.5.422 | 1.0.10.1 | A52FADCA | 4.15.5.14 | D486E623 | ? | 377417e7 | ? |
| 1.5.452 | 1.0.10.1 | A52FADCA | 4.15.5.14 | D486E623 | ? | 377417e7 | ? |
| 1.5.453 | 1.0.10.3 | 6094D118 | 4.15.5.14 | D486E623 | ? | 377417e7 | ? |
| 1.5.621 | 1.0.10.3 | 6094D118 | 4.15.5.14 | D486E623 | ? | 377417e7 | ? |
| 1.5.912 | 1.0.10.6 | C0453D59 | 4.15.5.14 | D486E623 | 0,2,5 | B061711F | ? |
| 1.6.122 | 1.0.10.11 | B2F80429 | 4.15.5.14 | D486E623 | 0,2,8 | 7AABD34F | ? |
| 1.6.352 | 1.0.10.14 | 89201DA3 | 4.15.5.14 | D486E623 | 0,2,8 | 7AABD34F | ? |
| 1.7.112 | 1.0.11.6 | 84E52E0E | 4.15.9.30 | 9B9A1FFC | 0,3,2 | 20F573A1 | ? |
| 1.7.421 | 1.0.11.6 | 84E52E0E | 4.15.9.30 | 9B9A1FFC | 0,3,2 | 20F573A1 | ? |
| 1.7.521 | 1.0.11.6 | 84E52E0E | 4.15.11.7 | A8F3A96E | 0,3,3 | 4CE91321 | ? |
| 1.7.611 | 1.0.11.6 | 84E52E0E | 4.15.11.13 | B853022E | 0,3,3 | 4CE91321 | ? |
| 1.7.811 | 1.0.11.6 | 84E52E0E | 4.15.11.20 | B4868C64 | 0,3,3 | 4CE91321 | ? |
| 1.8.111 | 1.0.11.7 | 237A8C9B | 4.15.11.20 | B4868C64 | 0,3,3 | 4CE91321 | ? |
| 1.8.441 | 1.0.11.7 | 237A8C9B | 4.15.11.20 | B4868C64 | 0,3,3 | 4CE91321 | ? |
| 1.8.511 | 1.0.12.0 | F6662DE3 | 4.15.12.10 | 393A9FC2 | 0,3,3 | 4CE91321 | ? |
| 1.8.711 | 1.0.12.0 | F6662DE3 | 4.15.12.10 | 393A9FC2 | 0,3,3 | 4CE91321 | ? |

In two latest versions of Mi Fit (1.8.511 and 1.8.711) was added new firmware file - HM05.fw

# Mili.hw

I'm not sure that this is correct

| offset | size | type | description |
|--------|------|------|-------------|
| 0x04 | 2 | offset ? | value 0x489 (for running.fw 0x4a1). After jump to the offset 48 80 47 0a (running: 48 80 47 15) |
| 0x40 | 2 | size | length of data - it starts after CRC?? |
| 0x64 | 2 | size? | some size? |
| 0x304 | 32 | text | device/processor name; filled with 0x0 |
| 0x37E | ? | text | always? RW-BLE |
| 0x39A | 32? | text | name of BT device |
| 0x420 | 6 | value | version (in running.fw is text, 8b?) |
| 0x438 | 8 | value | probably some CRC32 value. (In running.fw is filled with 0xFF) |
| 0x440 | X | data  | header? memory data...? |

# Mili_hr.fw

| offset | size | type | description |
|--------|------|------|-------------|
| 0x0 | 0x24 | data | header - only in Mili_hr.fr. Information about firmware for AMS AS7000 |
| 0x1A | 4 | offset | start heart rate biosensor firmware (AS7000) |
| 0x1E | 4 | size | size of heart rate biosensor firmware (AS7000) |


# NOTES
https://github.com/shesko/DA14580_HeartMonitor/blob/master/dk_apps/src/modules/app/src/app_project/sps/app_sps_device_project.h
