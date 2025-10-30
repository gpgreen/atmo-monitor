# atmo-monitor

KiCad design for a atmospheric measurement board. The MCU is a stm32f103
Series. There are 2 main sensors. One is the PMS2007, which measures
particulates, ie PM2.5. The other sensor is a BME680, which measures
temperature, pressure, and organic compounds. The measurements are output
on an E-Ink tri-color display.

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
is a 2-layer PCB that I have shared at [Oshpark](https://oshpark.com/shared_projects/8b0I1GvP).

## Changes

- Rev A
  Original

## Firmware

[Firmware](https://github.com/gpgreen/atmo-monitor-stm32)

## Connections to JTAG

I have put test points on the board, so that pogo pins can be used to program
the MCU.

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

## Credits

as always, thanks for the good work
- [Adafruit](https://www.adafruit.com)

## License

Licensed under

- MIT license ([LICENSE-MIT](LICENSE-MIT) or http://opensource.org/licenses/MIT)
