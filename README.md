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


Mili_hr.fw

| offset | size | type | description |
|--------|------|------|-------------|
| 0x0 | 0x24 | data | header - only in Mili_hr.fr. Information about firmware for AMS AS7000 |
| 0x1A | 4 | offset | start heart rate biosensor firmware (AS7000) |
| 0x1E | 4 | size | size of heart rate biosensor firmware (AS7000) |
