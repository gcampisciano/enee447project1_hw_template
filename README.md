# ENEE447 Project 1
## NOTE
**This code uses 32-bit cross-compiler which is different than the 64-bit cross-compiler we set up for project 0.**

## Environment setup
- SD card: format it to be FAT32 if you haven't done so
- 32-bit cross-compiler:
  - Ubuntu
    - Download [AArch32 bare-metal target (arm-none-eabi)](https://developer.arm.com/-/media/Files/downloads/gnu-a/9.2-2019.12/binrel/gcc-arm-9.2-2019.12-x86_64-arm-none-eabi.tar.xz?revision=64186c5d-b471-4c97-a8f5-b1b300d6594a&la=en&hash=5E9204DA5AF0B055B5B0F50C53E185FAA10FF625)
    - Modify `.bashrc` at the home directory, put this line at the end `export PATH=$PATH:/home/student/Desktop/gcc-arm-9.2-2019.12-x86_64-arm-none-eabi/bin/` (assuming you uncompressed the cross-compiler at `Desktop`)
    - Close all terminal windows and re-open one so that the configuration we just made in `.bashrc` will be in effect

## You're supposed to modify the following files
- Just need to put your name [here in kernel.c](https://github.com/sklaw/enee447project1_hw_template/blob/master/kernel.c#L28)

## Useful Readings
- [BCM2835 peripheral document](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2835/README.md): Raspberry Pi 3B+ is using BCM2837, but currently there is no official documentation for BCM2837 board:) So we have to use documents of BCM2835. **NOTE**: according this [site](https://www.raspberrypi.org/documentation/hardware/raspberrypi/peripheral_addresses.md), the peripheral addresses of pi 3 starts at `0x3F000000`. So when you are reading the BCM2835 document, replace `7E` with `3F` when you see a memory address.


## Steps to carry out for this experiment
1. Compile this code with `make` command, copy the files (not the folder) in `things_to_copy_to_your_sd_card` to your SD card, insert the SD card into your board but **don't boot your board yet**
1. Connect USB-serial cable with your board as follows
![USB-serial cable connection](https://github.com/sklaw/enee447project1_hw_template/blob/master/images_used_by_Readme/usbserialconnection.png "USB-serial cable connection")
1. Launch your communication program on your computer so that you can receive/transmit data from/to the board via UART.
    - **NOTE**: No matter what communication program you use, you should configure its **serial port setting** to be "baud rate=115200, parity=none, data=8, stop bits=1, hardware flow control=no, software flow control=no" because this is the UART configuration used in this code.
    - Example
        - Ubuntu: `minicom`
            - Plug the USB-serial connector to your computer. Use `ls -l /dev/ttyUSB0` to check if the USB is detected by Ubuntu. If not, you need to fix this :) (Contact TA)
            - Execute this in terminal: `sudo minicom -s`
            - ![](https://github.com/sklaw/enee447project1_hw_template/blob/master/images_used_by_Readme/minicomstep1.png)
            - ![](https://github.com/sklaw/enee447project1_hw_template/blob/master/images_used_by_Readme/minicomstep2.png)
            - ![](https://github.com/sklaw/enee447project1_hw_template/blob/master/images_used_by_Readme/minicomstep3.png)
            - ![](https://github.com/sklaw/enee447project1_hw_template/blob/master/images_used_by_Readme/minicomstep4.png)
            - ![](https://github.com/sklaw/enee447project1_hw_template/blob/master/images_used_by_Readme/minicomstep5.png)
            - If the image above shows up, then your `minicom` is launched properly. Now unplug the USB-serial connector then plug it again to your computer, which will reboot the board and you should see the following UART messages showing up in `minicom` ![](https://github.com/sklaw/enee447project1_hw_template/blob/master/images_used_by_Readme/minicomstep6.png)
            - Now if you type 'a', minicom will print 'A', which means the echo server is working and it's converting your input to uppercase.

