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
9. If you are using the Adafruit bonnet, it is time to connect it and go straight to the [Configuration](https://github.com/NestEggCrypto/pitrezor-firmware/blob/main/HowTo.md#configuration) section below. Otherwise, continue reading
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

21. Connect the SD card back to your computer and refer to the [configuration section](https://github.com/NestEggCrypto/pitrezor-firmware/blob/main/HowTo.md#configuration) below to correctly configure your OLED model and orientation. Their is only 2 possibles orientations so you can try both and see which one is better for you.
22. Reconnect everything and retry your device. Now you should see the output on the HDMI connector if connected and also on the OLED at the same time.
23. If that worked, put everything in a box!
24. Enjoy!

## Configuration
If you connect the SD card in your computer you should see a file named "`pitrezor.config`" in the first partition (boot partition). You can open this file with your favorite text editor. You will be able to change the configuration variables which are:

* `TREZOR_OLED_SCALE`: This control the scale factor of the display to apply when using the HDMI output. A scale factor of 1 means the default size of 128x64 pixel. A scale factor of 2 will stretch the image to 256x128 and so on.
* `TREZOR_OLED_TYPE`: Specify the type of OLED connected to the pi zero. The file enumerate the different value and their meaning. Select the one that match your OLED display.
* `TREZOR_OLED_FLIP`: Set to 0 or 1 to control the image vertically (normal or inverted) This is useful depending how you assemble the OLED in n enclosure.
* `TREZOR_GPIO_YES` and `TREZOR_GPIO_NO` : Specify the GPIO number to use for the yes/no button. If you soldered the buttons like mentionned in the tutorial, you can keep the default values.

When you change a value, keep the line formating as-is with the export statement. Just change the number after the equal sign. If you change something else, this could prevent the pi trezor application to start correctly.

# For the Adafruit bonnet, you must change the values to these:
* `export TREZOR_OLED_TYPE=1`
* `export TREZOR_OLED_FLIP=1`
* `export TREZOR_GPIO_YES=6`
* `export TREZOR_GPIO_NO=5`

## Is this secure ?
The main difference of this device versus the real trezor device is that the pi zero stores everything on the SD card. The equivalent of the flash memory for the trezor is stored in a file on the first partition. That means that anybody that has your SD card can access your seed words and private key.


However, the wallet supports the usage of a passphrase. The passphrase is a kind of an extra seed word that is not stored on SD card. By using a passphrase, you would prevent a thief that could have your SD card to empty your wallet.

Thus, the recommendation is to **__always use a passphrase__**!

## Updating from previous pitrezor image
If you are updating your pitrezor to the latest image you will need your seed words with you:

* Make sure that you have seed backup available. This mean your word list !! If not, you'll need to transfer all your funds to another wallet and disconnect other services (like U2F, password manager etc.
* Erase (Wipe) your pitrezor from trezor wallet or trezor suite application. This step improve the security before putting back the SD card in a PC in case it is infected.
* Put the SD card in a PC and copy your `pitrezor.config` file from the SD card to the computer
* Flash the SD card with the latest downloaded image
* Disconnect and reconnect the SD card to your computer
* Copy your `pitrezor.config` file from the computer to the SD card to overwrite the default version with your own version.
* Eject the SD card from your computer and install it in the pi zero
* Boot your pitrezor as usual
* When you will go to the wallet web site, your pitrezor will be detected as a new device. Select the recover option. You will have to enter all the words of your seed word list (advanced recovery mode is recommended so that your seed will never be entered on a computer).
* Don't forget to enable the passphrase option after if you were using one before. You should! If you haven't you can create new hidden wallet with a passphrase.
