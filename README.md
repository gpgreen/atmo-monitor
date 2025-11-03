# atmo-monitor

KiCad design for a atmospheric measurement board. The MCU is a
stm32f103cbt6. There are 2 main sensors. One is the PMS2007, which
measures particulates, ie PM2.5. The other sensor is a BME680, which
measures temperature, pressure, and organic compounds. The
measurements are output on an E-Ink tri-color display.

This design is a continuation of a project that I did using a nucleo dev board
and a perfboard pcb. The main goals used for this design:

    - Use smd devices that I had already for the rest of the project, instead of a dev board
    - Use an [Adafruit power supply breakout](https://www.adafruit.com/product/1944) that allows the use of a lithium battery. I didn't
    want to implement this on the PCB for this project, and I don't have those types of devices on hand.
    - Hand soldering for the pcb instead of my usual hot-plate reflow technique. This means
    using 1206 size components instead of 0603, and SO footprint parts. This also helps with
    the previous goal of using parts I had on hand, as my newer designs use TQFP footprints. I have successfully
    hand soldered the smaller parts, but it is very tedious.

I was able to finish the design with the goals and the only part I needed to purchase was the adafruit power breakout. It
is a 2-layer PCB that I have shared at [Oshpark](https://oshpark.com/shared_projects/oVsTK2Hw).

## Changes

- Rev A
  Original

## Firmware

[Firmware](https://github.com/gpgreen/atmo-monitor-stm32)

## Connections to Segger JTAG

I have put test points on the board, so that pogo pins can be used to program
the MCU.

[jlink web page](https://www.segger.com/products/debug-probes/j-link/technology/interface-description/)
```
**** 20 Pin connector for JTAG
                -------
    VTref      1|*   *|2 NC
    nTRST      3|*   *|4 GND
    TDI        5|*   *|6 GND
    TMS        7|*   *|8 GND
    TCK        9|*   *|10 GND
    RTCK      11|*   *|12 GND
    TDO       13|*   *|14 GND
    RESET     15|*   *|16 GND*
    DBGRQ     17|*   *|18 GND*
    5V Supply 19|*   *|20 GND*
                -------
```
From a 20pin JTAG connector, run wires to the following test pads to connect a debugger:
```
VTRef 1  <-> 3V3
SWDIO 7  <-> SWD
SWCLK 9  <-> SWC
RESET 15 <-> RST
GND   4  <-> GND
```

## Running SEGGER JLink

Run the JLink GDB server via the following:
```
JLinkGDBServer -if SWD -device STM32F103CB
```

GDB can be connected via the following:
```
gdb-multiarch --command=jlink-stm32.gdb target/thumbv7m/debug/main
```

## Running ocd
```
openocd -f interface/stlink-v3.cfg -f target/stm32f1x.cfg
```

## Credits

as always, thanks for the good work
- [Adafruit](https://www.adafruit.com)

## License

Licensed under

- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)
