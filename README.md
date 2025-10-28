# atmo-monitor

KiCad design for a atmospheric measurement board. The MCU is a stm32f103
Series. There are 2 main sensors. One is the PMS 2007, which measures
particulates, ie PM2.5. The other sensor is a BMS 680, which measures
temperature, pressure, and organic compounds.

## Changes

- Rev A
  Original

## Firmware

Firmware for the board

https://github.com/gpgreen/atmo-monitor-stm32

## Boot configuration

To boot from main flash [0x0800_0000]
  Connect J2-4 to J2-5 (or) solder JP5-1 to center post

To boot from System mem [0x1FFF_0000], or Embedded SRAM [0x2000_0000]
  Connect J2-4 to J2-3 (or) solder JP6-3 to center post

There is an embedded boot loader, programmed in production, in the system memory
block. See the reference manual 3.6.2.

## PIN JUMPER SIGNAL ASSIGNMENT
```
                    +-----+
            +--------------------+
            |J3     |     |    J2|
        VDD-|1      +-----+     1|-GND
        GND-|2                  2|-GND
       +3.3-|3                  3|-+3.3
[RESET] PF2-|4                  4|-PF4 [BOOT0_PRE]
[SWCLK]PA14-|5                  5|-GND
[SWDIO]PA13-|6                  6|-GND
        GND-|7       RST        7|-GND
        PF3-|8       +-+        8|-GND
        PA0-|9       |O|        9|-GND
        PA1-|10      +-+       10|-PB7
        PA2-|11                11|-PB6
        PA3-|12                12|-PB5
        PA4-|13                13|-PB4
        PA6-|14                14|-PB3
        PA6-|15   UPB          15|-PA15
        PA7-|16   +-+          16|-PA12 [USER LED - GREEN]
        PB0-|17   |O|          17|-PA11 [USER PUSHBUTTON]
        PB1-|18   +-+          18|-PA8
            |                    |
            +--------------------+
```
## Connections to JTAG

From a 20pin JTAG connector, run wires to the following pins to connect a debugger:

VTRef 1  <-> J3-3
SWDIO 7  <-> J3-6
SWCLK 9  <-> J3-5
RESET 15 <-> J3-4
5V    19 <-> NC
GND   4  <-> J3-2
GND   20 <-> J3-7

## Running SEGGER JLink

Run the JLink GDB server via the following:
```
JLinkGDBServer -if SWD -JLinkDevicesXMLPath ~/.config/SEGGER/JLinkDevices/Puya/PY32/JLinkDevices.xml -device PY32F030xx8
```

GDB can be connected via the following:
```
gdb-multiarch --command=jlink-py32.gdb target/thumbv6m/debug/blink-py32
```

## Links
- [Firmware](https://github.com/gpgreen/atmo-monitor-stm32)
