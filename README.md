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

For LinuxCNC on a Raspberry Pi the HAL driver for the GPIOs is this one: [Generic driver for any GPIO supported by gpiod](https://linuxcnc.org/docs/devel/html/drivers/hal_gpio.html).

In order to make all GPUs available you must disable the I2C and UART interface (which may be enabled by default).

Edit the 'config.txt':
```
sudo nano /boot/firmware/config.txt
```
Edit or add the two lines:
```
enable_uart=0
dtparam=i2c_arm=off
```
Reboot the Raspberry Pi `sudo reboot now`


#### GPIO mapping 
The GPIO mapping (using the above HAL driver) for this Raspberry Pi board is:

| GPIO | Function |
| ------------- | ------------- |
|"GPIO2"| Input 1 |
|"GPIO3"| Relay ON |
|"GPIO4"| Input 2 |
|"GPIO5"| Y dir |
|"GPIO6"| Spare |
|"GPIO7"| Z pulse |
|"GPIO8"| Z dir |
|"GPIO9"| Input 7 |
|"GPIO10"| Input 6 |
|"GPIO11"| Input 8 |
|"GPIO12"| PWM0-VFD |
|"GPIO13"| PWM1-FET |
|"GPIO14"| Output 5 (spare) |
|"GPIO15"| Output 4 (B dir) |
|"GPIO16"| Y pulse |
|"GPIO17"| Input 3 |
|"GPIO18"| Output 3 (B pulse) |
|"GPIO19"| V-Out2 |
|"GPIO20"| X dir |
|"GPIO21"| X pulse |
|"GPIO22"| Input 5 |
|"GPIO23"| Output 2 (A dir) |
|"GPIO24"| Output 1 (A pulse) |
|"GPIO25"| Enable motors |
|"GPIO26"| V-Out1 |
|"GPIO27"| Input 4 |
 
## License
When I made the decision to share this project I intended to make it public, but recent developments have changed that intention.
So, for now I will not share the hardware schematics.

There will be two version of this hat that can be purchased:
- A _full assembled_ version fully populated.
- A _semi assembled_ version populated with only the SMD components and you can solder the connecting heads yourself.
.
