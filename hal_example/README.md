
# Rpi2Cnc - HAL setup on LinuxCNC

# Work in progress 
# Rpi2Cnc - HAL setup on LinuxCNC

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
 
