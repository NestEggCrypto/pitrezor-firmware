## How To guide

PiTrezor : A DIY NestEGG Coin hardware wallet based on trezor and raspberry pi zero/ raspberry pi 4

The trezor is a hardware bitcoin and other cryptocurrency wallet made by satoshilabs used to secure online transactions. The security reside in the fact that the private key used to sign a transaction never leave the device to your computer.


The hardware wallet device connect via USB to a host computer. Any transaction that would imply sending money to someone must be signed to be considered valid by the cryptocurrency network, like the bitcoin network. To perform that, the transaction is sent to the hardware wallet device via USB. The user can confirm its authenticity on the device display and press a button on the device to sign it with the private key. The hardware wallet device will send back the signed transaction to the computer to be broadcasted to the internet. In this process, the private key is never accessed by the computer.

On the other hand, the raspberry pi zero is a low cost and small but powerful computer. You can buy one for about 5$. It is used on numerous projects by ton of developers and hobbyists around the world.

In this web page I will show you how to create your own hardware bitcoin wallet based on the original trezor source code and that run on it on a raspberry pi zero (or pi 4). This is a fun, low cost, D.I.Y. project for any cryptocurrency enthusiasm!


## Features:
* Low cost parts
* Easy to build if an existing raspberry pi hat is used
* Run on pi zero and pi 4.
* Use the original trezor One code. Only a thin layer is used to adapt the code to the raspberry pi Linux platform. 
* All code modifications are open source, like the original trezor code.
* 100% Compatible with trezor web wallet to perform transactions.
* Use the hardware random number generator of the raspberry pi for more security.
* Can be very secure if you use a pass phrase (see security section below)
* Support small OLED display and/or display via HDMI output.
* Adjustable display scale factor on HDMI output
* Fast boot (around 5 seconds)
* Software is free (but donations are accepted!)

## Quick start guide:
# List of required components:
* A raspberry pi zero. You don't need the pi zero W, it cost probably a little bit more than the regular pi zero, but it will work anyway. The difference is that pi zero W has wifi and bluetooth but this project don't use it. The network drivers are not loaded by the platform so the W can be considered as secure. As mentionnend, you can use a pi 4 also if you already have one but it is more expensive than the pi 0.
* An SD card. The image to write on the SD card is very small (around 100 Megs) so virtually any decent SD card should work. Make sure you have one that is compatible with the pi.
* A good micro-usb to usb cable.
* A mini HDMI male to HDMI female adapter to verify the output via the HDMI output. You need HDMI cable and a TV or monitor too!
* Two push buttons (normally open contact, SPST)
* Some wires to solder the buttons to the pi.
* Optionally, an I2C or SPI OLED display. Supported OLED are based on the SH1106 controller or Adafruit controller.
* Optionally, a box or enclosure for a more professional look. 
`You will also need standard tool like solder iron, pliers`

Of course, If you are using the Adafruit bonnet, you don't need separate push buttons or OLED. Refer to Hat documentation about how to connect the bonnet to the pi zero.

## Step-By-Step instructions:
1. If you don't have the software called "etcher" already installed in your computer, download it [here](https://etcher.io/) . This software is used to write the program image to the SD card.
2. [Download](https://github.com/NestEggCrypto/pitrezor) the latest pitrezor SD card image by clicking here and select "save" to save the zip file
3. Start etcher and follow the instructions. You will need to connect the SD card to your computer to flash the pitrezor image file.
4. After the card is flashed, put it in the SD card slot in the pi.
5. Connect the HDMI output to a monitor or tv using the cable and adapter. On the pi 4, use the mini HDMI connector just beside the usb-c connector.
6. Connect the USB cable in the USB port near the center of the pi, not the one near the corner. Refer to next picture. For the pi 4, the usb-c connector is used.

<img src="/img/pizero_usb_cable.jpg" style="width:100%!important;"/>

7. Connect the other end of the USB cable to your computer or a USB power supply. You should see the pi boot sequence in the monitor and after 4-5 seconds the trezor logo should appear. Good! That confirms that your pi and SD card are working correctly.
8. At this point you cannot do much, so disconnect the USB cable, HDMI adapter and cable and remove SD card.
9. If you are using the Adafruit bonnet, it is time to connect it and go straight to the "Configuration" section below. Otherwise, continue reading
10. Solder the 2 buttons to the pi as showed in the following diagram. The left button (called "no") is connected to the pins 30 and 32 (in yellow in the next picture). The right button (called "yes") is connected to the pins 34 and 36 (in red in the picture). This is the default setup but can be tweaked from configuration file. The pi 4 use the same pins.

<img src="/img/pizero_gpio_schema.jpg" style="width:100%!important;"/>

11.  Put back the SD card in the pi and reconnect the HDMI and USB cable back to your computer.
12. It should boot again, otherwise that means something went bad during the soldering of the buttons :(
13. Open a browser on your computer and navigate to [wallet.trezor.io](https://wallet.trezor.io)
14. You will be requested to install the trezor bridge if you never did it before. Select your operating system to download the correct bridge software and perform installation. If you plan to use the chrome brower, the bridge installation can be skipped.
15. If you installed the bridge, close and reopen your browser and go back to [wallet.trezor.io](https://wallet.trezor.io)
16. If you don't plan to use the bridge on Linux, don't forget to set the permission accordingly. Refer to [setting up chrome on linux](https://wiki.trezor.io/User_manual:Setting_up_the_Chrome_extension_on_Linux). 
17. If the bridge is already installed, you should see a message that invites you to connect your trezor. Connect the USB cable of your pi.
18. The browser application should detect the device and invite you to perform the trezor setup.
19. During the setup you will need the buttons to, at least, go from one seed word to another.
20. If all is working correctly you can disconnect everything to solder the OLED display. The I2C OLED display need 4 wires to solder and the SPI OLED uses 7 wires. Refer to the next picture to determine how to solder the OLED depending on interface. The pins are the same for the pi 4:

<img src="/img/pitrezor_oled_pinout.jpg" style="width:100%!important;"/>

21. Connect the SD card back to your computer and refer to the [configuration section]() below to correctly configure your OLED model and orientation. Their is only 2 possibles orientations so you can try both and see which one is better for you.
22. Reconnect everything and retry your device. Now you should see the output on the HDMI connector if connected and also on the OLED at the same time.
23. If that worked, put everything in a box!
24. Enjoy!

## Configuration