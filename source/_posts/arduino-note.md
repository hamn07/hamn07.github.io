title: arduino筆記區
date: 2015-08-27 14:01:13
tags:
---
<!-- toc -->

[林老師的教作業郵件](mailto://homeworks.iii@gmail.com)


# Syntax
[Memory](http://playground.arduino.cc/Learning/Memory)
[Port Registers](https://www.arduino.cc/en/Reference/PortManipulation)
[What is the difference between Serial.write and Serial.print? And when are they used?](http://arduino.stackexchange.com/questions/10088/what-is-the-difference-between-serial-write-and-serial-print-and-when-are-they)

# IDE
[Stino is a Sublime Text plugin that provides an Arduino-like environement for editing, compiling and uploading sketches.](https://github.com/Robot-Will/Stino)


# lib location
/Applications/Arduino.app/Contents/Java/libraries

```bash
✔ /Applications/Arduino.app/Contents/Java/hardware/arduino/avr/cores/arduino
21:09 $ ls -al
total 640
drwxr-xr-x@ 45 HamnLee  staff   1530  7 20 14:03 .
drwxr-xr-x@  3 HamnLee  staff    102  7 20 14:03 ..
-rw-r--r--@  1 HamnLee  staff   7286  7 20 14:03 Arduino.h
-rw-r--r--@  1 HamnLee  staff   5867  7 20 14:03 CDC.cpp
-rw-r--r--@  1 HamnLee  staff   1529  7 20 14:03 Client.h
-rw-r--r--@  1 HamnLee  staff  13744  7 20 14:03 HID.cpp
-rw-r--r--@  1 HamnLee  staff   7783  7 20 14:03 HardwareSerial.cpp
-rw-r--r--@  1 HamnLee  staff   4875  7 20 14:03 HardwareSerial.h
-rw-r--r--@  1 HamnLee  staff   2605  7 20 14:03 HardwareSerial0.cpp
-rw-r--r--@  1 HamnLee  staff   2315  7 20 14:03 HardwareSerial1.cpp
-rw-r--r--@  1 HamnLee  staff   1975  7 20 14:03 HardwareSerial2.cpp
-rw-r--r--@  1 HamnLee  staff   1975  7 20 14:03 HardwareSerial3.cpp
-rw-r--r--@  1 HamnLee  staff   4469  7 20 14:03 HardwareSerial_private.h
-rw-r--r--@  1 HamnLee  staff   1993  7 20 14:03 IPAddress.cpp
-rw-r--r--@  1 HamnLee  staff   2715  7 20 14:03 IPAddress.h
-rw-r--r--@  1 HamnLee  staff   5371  7 20 14:03 Print.cpp
-rw-r--r--@  1 HamnLee  staff   2614  7 20 14:03 Print.h
-rw-r--r--@  1 HamnLee  staff   1335  7 20 14:03 Printable.h
-rw-r--r--@  1 HamnLee  staff    963  7 20 14:03 Server.h
-rw-r--r--@  1 HamnLee  staff   8677  7 20 14:03 Stream.cpp
-rw-r--r--@  1 HamnLee  staff   5111  7 20 14:03 Stream.h
-rw-r--r--@  1 HamnLee  staff  15010  7 20 14:03 Tone.cpp
-rw-r--r--@  1 HamnLee  staff   6805  7 20 14:03 USBAPI.h
-rw-r--r--@  1 HamnLee  staff  14010  7 20 14:03 USBCore.cpp
-rw-r--r--@  1 HamnLee  staff   7855  7 20 14:03 USBCore.h
-rw-r--r--@  1 HamnLee  staff   1872  7 20 14:03 USBDesc.h
-rw-r--r--@  1 HamnLee  staff   4180  7 20 14:03 Udp.h
-rw-r--r--@  1 HamnLee  staff   4576  7 20 14:03 WCharacter.h
-rw-r--r--@  1 HamnLee  staff   9342  7 20 14:03 WInterrupts.c
-rw-r--r--@  1 HamnLee  staff   1650  7 20 14:03 WMath.cpp
-rw-r--r--@  1 HamnLee  staff  16825  7 20 14:03 WString.cpp
-rw-r--r--@  1 HamnLee  staff   9591  7 20 14:03 WString.h
-rw-r--r--@  1 HamnLee  staff   1222  7 20 14:03 abi.cpp
-rw-r--r--@  1 HamnLee  staff  11214  7 20 14:03 binary.h
-rw-r--r--@  1 HamnLee  staff   1142  7 20 14:03 hooks.c
-rw-r--r--@  1 HamnLee  staff   1312  7 20 14:03 main.cpp
-rw-r--r--@  1 HamnLee  staff   1027  7 20 14:03 new.cpp
-rw-r--r--@  1 HamnLee  staff    979  7 20 14:03 new.h
-rw-r--r--@  1 HamnLee  staff  12103  7 20 14:03 wiring.c
-rw-r--r--@  1 HamnLee  staff   7751  7 20 14:03 wiring_analog.c
-rw-r--r--@  1 HamnLee  staff   5030  7 20 14:03 wiring_digital.c
-rw-r--r--@  1 HamnLee  staff   2147  7 20 14:03 wiring_private.h
-rw-r--r--@  1 HamnLee  staff   6022  7 20 14:03 wiring_pulse.S
-rw-r--r--@  1 HamnLee  staff   3631  7 20 14:03 wiring_pulse.c
-rw-r--r--@  1 HamnLee  staff   1601  7 20 14:03 wiring_shift.c
```
```bash
ls -✔ /Applications/Arduino.app/Contents/Java/hardware/arduino/avr/libraries
21:16 $ ls -al
total 0
drwxr-xr-x@  6 HamnLee  staff  204  7 20 14:03 .
drwxr-xr-x@ 10 HamnLee  staff  340  7 20 14:03 ..
drwxr-xr-x@  7 HamnLee  staff  238  7 20 14:03 EEPROM
drwxr-xr-x@  7 HamnLee  staff  238  7 20 14:03 SPI
drwxr-xr-x@  7 HamnLee  staff  238  7 20 14:03 SoftwareSerial
drwxr-xr-x@  8 HamnLee  staff  272  7 20 14:03 Wire
```

```bash
✔ /Applications/Arduino.app/Contents/Java/hardware/tools/avr/avr/include
21:40 $ tree .
.
├── alloca.h
├── assert.h
├── avr
│   ├── boot.h
│   ├── builtins.h
│   ├── common.h
│   ├── cpufunc.h
│   ├── crc16.h
│   ├── delay.h
│   ├── eeprom.h
│   ├── fuse.h
│   ├── interrupt.h
│   ├── io.h
│   ├── io1200.h
│   ├── io2313.h
│   ├── io2323.h
│   ├── io2333.h
│   ├── io2343.h
│   ├── io43u32x.h
│   ├── io43u35x.h
│   ├── io4414.h
│   ├── io4433.h
│   ├── io4434.h
│   ├── io76c711.h
│   ├── io8515.h
│   ├── io8534.h
│   ├── io8535.h
│   ├── io86r401.h
│   ├── io90pwm1.h
│   ├── io90pwm161.h
│   ├── io90pwm216.h
│   ├── io90pwm2b.h
│   ├── io90pwm316.h
│   ├── io90pwm3b.h
│   ├── io90pwm81.h
│   ├── io90pwmx.h
│   ├── io90scr100.h
│   ├── ioa5272.h
│   ├── ioa5505.h
│   ├── ioa5702m322.h
│   ├── ioa5782.h
│   ├── ioa5790.h
│   ├── ioa5790n.h
│   ├── ioa5795.h
│   ├── ioa5831.h
│   ├── ioa6285.h
│   ├── ioa6286.h
│   ├── ioa6289.h
│   ├── ioa6612c.h
│   ├── ioa6613c.h
│   ├── ioa6614q.h
│   ├── ioa6616c.h
│   ├── ioa6617c.h
│   ├── ioa664251.h
│   ├── ioat94k.h
│   ├── iocan128.h
│   ├── iocan32.h
│   ├── iocan64.h
│   ├── iocanxx.h
│   ├── iom103.h
│   ├── iom128.h
│   ├── iom1280.h
│   ├── iom1281.h
│   ├── iom1284.h
│   ├── iom1284p.h
│   ├── iom1284rfr2.h
│   ├── iom128a.h
│   ├── iom128rfa1.h
│   ├── iom128rfr2.h
│   ├── iom16.h
│   ├── iom161.h
│   ├── iom162.h
│   ├── iom163.h
│   ├── iom164.h
│   ├── iom164a.h
│   ├── iom164p.h
│   ├── iom164pa.h
│   ├── iom165.h
│   ├── iom165a.h
│   ├── iom165p.h
│   ├── iom165pa.h
│   ├── iom168.h
│   ├── iom168a.h
│   ├── iom168p.h
│   ├── iom168pa.h
│   ├── iom168pb.h
│   ├── iom169.h
│   ├── iom169a.h
│   ├── iom169p.h
│   ├── iom169pa.h
│   ├── iom16a.h
│   ├── iom16hva.h
│   ├── iom16hva2.h
│   ├── iom16hvb.h
│   ├── iom16hvbrevb.h
│   ├── iom16m1.h
│   ├── iom16u2.h
│   ├── iom16u4.h
│   ├── iom2560.h
│   ├── iom2561.h
│   ├── iom2564rfr2.h
│   ├── iom256rfr2.h
│   ├── iom3000.h
│   ├── iom32.h
│   ├── iom323.h
│   ├── iom324a.h
│   ├── iom324p.h
│   ├── iom324pa.h
│   ├── iom325.h
│   ├── iom3250.h
│   ├── iom3250a.h
│   ├── iom3250p.h
│   ├── iom3250pa.h
│   ├── iom325a.h
│   ├── iom325p.h
│   ├── iom325pa.h
│   ├── iom328.h
│   ├── iom328p.h
│   ├── iom329.h
│   ├── iom3290.h
│   ├── iom3290a.h
│   ├── iom3290pa.h
│   ├── iom329a.h
│   ├── iom329p.h
│   ├── iom329pa.h
│   ├── iom32a.h
│   ├── iom32c1.h
│   ├── iom32hvb.h
│   ├── iom32hvbrevb.h
│   ├── iom32m1.h
│   ├── iom32u2.h
│   ├── iom32u4.h
│   ├── iom32u6.h
│   ├── iom406.h
│   ├── iom48.h
│   ├── iom48a.h
│   ├── iom48p.h
│   ├── iom48pa.h
│   ├── iom48pb.h
│   ├── iom64.h
│   ├── iom640.h
│   ├── iom644.h
│   ├── iom644a.h
│   ├── iom644p.h
│   ├── iom644pa.h
│   ├── iom644rfr2.h
│   ├── iom645.h
│   ├── iom6450.h
│   ├── iom6450a.h
│   ├── iom6450p.h
│   ├── iom645a.h
│   ├── iom645p.h
│   ├── iom649.h
│   ├── iom6490.h
│   ├── iom6490a.h
│   ├── iom6490p.h
│   ├── iom649a.h
│   ├── iom649p.h
│   ├── iom64a.h
│   ├── iom64c1.h
│   ├── iom64hve.h
│   ├── iom64hve2.h
│   ├── iom64m1.h
│   ├── iom64rfr2.h
│   ├── iom8.h
│   ├── iom8515.h
│   ├── iom8535.h
│   ├── iom88.h
│   ├── iom88a.h
│   ├── iom88p.h
│   ├── iom88pa.h
│   ├── iom88pb.h
│   ├── iom8a.h
│   ├── iom8hva.h
│   ├── iom8u2.h
│   ├── iomx8.h
│   ├── iomxx0_1.h
│   ├── iomxx4.h
│   ├── iomxxhva.h
│   ├── iotn10.h
│   ├── iotn11.h
│   ├── iotn12.h
│   ├── iotn13.h
│   ├── iotn13a.h
│   ├── iotn15.h
│   ├── iotn1634.h
│   ├── iotn167.h
│   ├── iotn20.h
│   ├── iotn22.h
│   ├── iotn2313.h
│   ├── iotn2313a.h
│   ├── iotn24.h
│   ├── iotn24a.h
│   ├── iotn25.h
│   ├── iotn26.h
│   ├── iotn261.h
│   ├── iotn261a.h
│   ├── iotn28.h
│   ├── iotn4.h
│   ├── iotn40.h
│   ├── iotn4313.h
│   ├── iotn43u.h
│   ├── iotn44.h
│   ├── iotn441.h
│   ├── iotn44a.h
│   ├── iotn45.h
│   ├── iotn461.h
│   ├── iotn461a.h
│   ├── iotn48.h
│   ├── iotn5.h
│   ├── iotn828.h
│   ├── iotn84.h
│   ├── iotn841.h
│   ├── iotn84a.h
│   ├── iotn85.h
│   ├── iotn861.h
│   ├── iotn861a.h
│   ├── iotn87.h
│   ├── iotn88.h
│   ├── iotn9.h
│   ├── iotnx4.h
│   ├── iotnx5.h
│   ├── iotnx61.h
│   ├── iousb1286.h
│   ├── iousb1287.h
│   ├── iousb162.h
│   ├── iousb646.h
│   ├── iousb647.h
│   ├── iousb82.h
│   ├── iousbxx2.h
│   ├── iousbxx6_7.h
│   ├── iox128a1.h
│   ├── iox128a1u.h
│   ├── iox128a3.h
│   ├── iox128a3u.h
│   ├── iox128a4u.h
│   ├── iox128b1.h
│   ├── iox128b3.h
│   ├── iox128c3.h
│   ├── iox128d3.h
│   ├── iox128d4.h
│   ├── iox16a4.h
│   ├── iox16a4u.h
│   ├── iox16c4.h
│   ├── iox16d4.h
│   ├── iox16e5.h
│   ├── iox192a3.h
│   ├── iox192a3u.h
│   ├── iox192c3.h
│   ├── iox192d3.h
│   ├── iox256a3.h
│   ├── iox256a3b.h
│   ├── iox256a3bu.h
│   ├── iox256a3u.h
│   ├── iox256c3.h
│   ├── iox256d3.h
│   ├── iox32a4.h
│   ├── iox32a4u.h
│   ├── iox32c3.h
│   ├── iox32c4.h
│   ├── iox32d3.h
│   ├── iox32d4.h
│   ├── iox32e5.h
│   ├── iox384c3.h
│   ├── iox384d3.h
│   ├── iox64a1.h
│   ├── iox64a1u.h
│   ├── iox64a3.h
│   ├── iox64a3u.h
│   ├── iox64a4u.h
│   ├── iox64b1.h
│   ├── iox64b3.h
│   ├── iox64c3.h
│   ├── iox64d3.h
│   ├── iox64d4.h
│   ├── iox8e5.h
│   ├── lock.h
│   ├── parity.h
│   ├── pgmspace.h
│   ├── portpins.h
│   ├── power.h
│   ├── sfr_defs.h
│   ├── signal.h
│   ├── signature.h
│   ├── sleep.h
│   ├── version.h
│   ├── wdt.h
│   └── xmega.h
├── compat
│   ├── deprecated.h
│   ├── ina90.h
│   └── twi.h
├── ctype.h
├── errno.h
├── inttypes.h
├── math.h
├── setjmp.h
├── stdfix-avrlibc.h
├── stdint.h
├── stdio.h
├── stdlib.h
├── string.h
└── util
    ├── atomic.h
    ├── crc16.h
    ├── delay.h
    ├── delay_basic.h
    ├── parity.h
    ├── setbaud.h
    └── twi.h
```
