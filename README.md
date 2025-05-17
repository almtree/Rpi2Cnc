# Rpi2Cnc

***Rpi-2-Cnc*** is an HAT for the ***Raspberry Pi 4 and 5*** that directly exposed the GPIOs pins to control Stepper Drivers, Limit Switches, Inputs, PWM Spindle, VFD, Relay, etc to the ***LinuxCNC HAL interface***.

I made this board since all the solutions that I found to interface the LinuxCNC controller software and the CNC hardware using a Raspberry Pi envolved the use of a board on the Rpi to convert the GPIOs to the parallel interface, and then use a second board to interface the Parallel port with the CNC hardware itself.

## Hardware
I designed this board taking into account the hardware I already had to control the CNC, namely DM556T stepper drivers, a VFD spindler and active low home and limit switches, up to 5 axes can be controlled and the outputs used for this are open collector type, which opens up a wide range of stepper controllers. 

### Main features 
- 10 open collector outputs for 5 axis (step/dir interface)
- 1 open collector output for steppers ENABLE
- P-Mosfet PWM controled (up to 40V and 20Amps)
- 0-10V VFD control from PWM
- Relay output (up to 230V and 10Amps)
- 2 VCC outputs (500mA and 1.5Amps)
- 8 inputs with hardware debounce and external pull-up (active low, can be inverted in software)
- 12 to 24V power IN
- Included DC-DC step down buck converter to power RPi and 5V rail
 
## Software and HAL driver
The main CNC control software is off course LinuxCN. I won't go into detail about what it is, how it works or how to install LinuxCNC on a Raspberru Pi, You can find all this information on the [LinuxCNC website](https://linuxcnc.org/)

### HAL driver
Hardware Abstraction Layer (HAL) is a software layer that provides hardware abstraction for operating systems such as UNIX. In short, it allows programs like LinuxCNC to use any hardware by using a driver.



enable_uart=0
dtparam=i2c_arm=off

dtparam=i2c_arm=on

For LinuxCNC on a Raspberry Pi the HAL driver for the GPIOs is this one: [Generic driver for any GPIO supported by gpiod](https://linuxcnc.org/docs/devel/html/drivers/hal_gpio.html).

#### GPIO mapping 
The GPIO mapping (using the above HAL driver) for this Raspberry Pi board is:
        line   0:     "ID_SDA"       unused   input  active-high
        line   1:     "ID_SCL"       unused   input  active-high
        line   2:      "GPIO2"       unused   input  active-high
        line   3:      "GPIO3"       unused   input  active-high
        line   4:      "GPIO4"       unused   input  active-high
        line   5:      "GPIO5"       unused   input  active-high
        line   6:      "GPIO6"       unused   input  active-high
        line   7:      "GPIO7"       unused   input  active-high
        line   8:      "GPIO8"       unused   input  active-high
        line   9:      "GPIO9"       unused   input  active-high
        line  10:     "GPIO10"       unused   input  active-high
        line  11:     "GPIO11"       unused   input  active-high
        line  12:     "GPIO12"       unused   input  active-high
        line  13:     "GPIO13"       unused   input  active-high
        line  14:     "GPIO14"       unused   input  active-high
        line  15:     "GPIO15"       unused   input  active-high
        line  16:     "GPIO16"       unused   input  active-high
        line  17:     "GPIO17"       unused   input  active-high
        line  18:     "GPIO18"       unused   input  active-high
        line  19:     "GPIO19"       unused   input  active-high
        line  20:     "GPIO20"       unused   input  active-high
        line  21:     "GPIO21"       unused   input  active-high
        line  22:     "GPIO22"       unused   input  active-high
        line  23:     "GPIO23"       unused   input  active-high
        line  24:     "GPIO24"       unused   input  active-high
        line  25:     "GPIO25"       unused   input  active-high
        line  26:     "GPIO26"       unused   input  active-high
        line  27:     "GPIO27"       unused   input  active-high
 






## License
When I made the decision to share this project I intended to make it public, but recent developments have changed that intention.
So, for now I will not share the hardware schematics.

There will be two version of this hat that can be purchased:
- A _full assembled_ version fully populated.
- A _semi assembled_ version populated with only the SMD components and you can solder the connecting heads yourself.
.
