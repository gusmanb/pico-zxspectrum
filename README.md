# pico-zxspectrum
48k/128k ZX Spectrum for Raspberry Pico Pi RP2040

<a href="docs/1280px-ZXSpectrum48k.jpg"><img src="docs/640px-ZXSpectrum48k.png" height="200"/></a><a href="docs/1280px-ZX_Spectrum128K.jpg"><img src="docs/640px-ZX_Spectrum128K.png" height="200"/></a>

## Features
* DVI over HDMI ([Wren's Amazing PicoDVI](https://github.com/Wren6991/PicoDVI))
* LCD support (ST7789 320x240)
* VGA video (RGB332, RGB222, RGBY1111)
* USB keyboard & Joysticks
* PS/2 keyboard
* Martix keyboard
* PWM/I2S DAC audio for 48k buzzer and AY-3-8912
* Audio input (load from tape)
* 12 quick save slots
* Load from .z80 snapshot files
* Read from .tap & .tzx tape files
* On screen menu system
* Kempston and Sinclair joystick emulation

## Supported Boards
Click on the images below for mnore inforation about a particular board...

The idea of this project is for it to be relatively easy to breadboard or prototype in some way. It's just for fun and not a highly accurate emulation; hopefully it is good enough to be enjoyable.

<table>
  <tr>
    <td>
      <a href="docs/ZxSpectrumBreadboardHdmiKbd1PinAudio.md">
<img src="docs/proto_kbd.jpg" width="200"/>
      </a>
    </td>
    <td>
      <a href="docs/ZxSpectrumBreadboardHdmiNPinAudio.md">
        <img src="docs/pico_zxspectrum_prototype_1.jpg" width="200"/>
      </a>
      <a href="docs/ZxSpectrum4PinAudioVga1111Ps2.md">
        <img src="docs/ZxSpectrum4PinAudioVga1111Ps2Breadboard.jpg" width="200"/>
      </a>
    </td>
  </tr>
</table>

<br/>
There are now a variety of boards that are also supported...

<a href="docs/pico_zx48_128.md"><img src="docs/pico_zx48_128_1.png" width="300"/></a>
<a href="docs/ZxSpectrumPicomputerZxLcd.md"><img src="docs/picozxlcd.png" width="280"/></a>
<a href="docs/ZxSpectrumPicomputerVga222Zx.md"><img src="docs/picomputer_picozx.png" width="300"/></a>
<a href="docs/ZxSpectrumPicomputerVga.md" width="200"/></a>
<a href="docs/ZxSpectrumPicomputerMax.md"><img src="docs/picomputermax.png" width="200"/></a>
<a href="docs/ZxSpectrumPicomputerZX.md"><img src="docs/picomputerzx.png" width="200"/></a>
<a href="docs/ZxSpectrumPicoDv.md"><img src="docs/P1040672_1500x1500.png" width="200"/></a>
<a href="docs/ZxSpectrumPicaVga.md"><img src="docs/pico-demo-base-9_1500x1500.png" width="200"/></a>
<a href="docs/MURMULATOR.md"><img src="docs/MURMULATOR_VGA_photo1.png" width="200"/></a>

## Interesting projects
[Hermit Retro Products](https://mk-mk.facebook.com/hermitretro/)<br>

## Updates
11/02/24 
* Start to separate out docs for each target
* Initial support for ILI9341

20/01/24 - Maintenance release of pre-built firmware: 
* All .uf2 files rebuilt (see the uf2 folder)
* Minor bug fixes
* Updated libraries (Z80 etc)
* Misc joystick fixes
  
I've moved to a new build machine, so let me know if there are any issues.
At some point, I will try and organise the spralling README file.
  
01/01/24 - Added support for bobricius <a href="docs/pico_zx48_128">Pico ZX48/128</a>

25/06/23 - Ability to persist volume control and joystick type (Sinclair/Kempston). The settings are persisted to .config file on the SD card and are loaded as the defaults on reset.
To save setting goto ''settings->save'' on the menu. 
I was hoping to save to flash memory but not got that to work as of yet.
        
04/06/23 - Add MURMULATOR platform, with thanks to [Javavi](https://github.com/javavi) 

03/06/23 - Don't freeze on startup if no SD card is present. Release v0.33

29/04/23 - Added new target for Bobricious PICOZX LCD + general release v0.32
* PICOZX with LCD can now use either the LCD or VGA output
* Volume control (for target where it makes sense)
* Some changes to key mappings and menu navigation

To boot into VGA mode hold down the 'fire' button during reset.

The key mapping changes were intended to make navigating the menus with a joystick a bit easier.
In particular, now left (usually) goes 'back' and right enters/activates an item. 
Paging in the file-explorer is now achieved with the Page-Up and Page-Down keys.
Not sure it will stay like this; mapping keys and directions in a way that works for the emulator and the menus can be tricky.

19/01/23 - Added new target for [ArnoldUK](https://github.com/ArnoldUK).
This target can read from a standard 48k Spectrum keyboard matrix.

25/12/22 - Very basic support for sub-folders in the 'snapshots' and 'tapes' storage areas has been added.
Files can be renamed, copied and deleted from the menu system.
The quick-saves folder is now under the snapshots folder and behaves just like any other folder.
The file 'explorer' has the following commands:
* &lt;space&gt;/&lt;enter&gt; - enter a folder/load a file
* ESC   - Go up a folder
* 1=DEL - Delete the file
* 2=REN - Rename the file
* 3=CPY - Copy the file
* 4=PST - Paste the file
* 5=REF - Reload the list of files in the current folder

The function keys for playing tapes have been removed. 
The idea is that in the future more useful controls will be added like 'play', 'stop' and 'eject'.

5/12/22 - The emulator can now cope with more files in the snapshots and tapes folders without running out of memory.
I've tested up to 400 but it may survive more that this.
Directory entries are now written to a file .dcache which can be updated from the menus by 'rescanning' the folder.
If you are adding files to the folders on a PC you can just delete the .dcache and it will get regenerated on next power-on.

I've moved to the [Redcode Z80 emulator](https://github.com/redcode/Z80) as:
* It comes with a test suite
* It is much faster than the previous emulator

TZX support added with some omissions:
* No CSW support (raise an issue if this is important to you)
* There are some compatiblity issues

Builds with an RP_AUDIO_IN pin can now load from tape. 
Preparing the audio signal will require a little extra circuitry and some examples will be added to this page.

The move from [Carl's no-OS-FatFS-SD-SPI-RPi-Pico](https://github.com/carlk3/no-OS-FatFS-SD-SPI-RPi-Pico) to 
[Pimoroni's FatFS](https://github.com/pimoroni/pimoroni-pico) was made as the SD card pins on the 
[Pimoroni Pico DV Demo Base](https://shop.pimoroni.com/products/pimoroni-pico-dv-demo-base) do not match up with the
RP2040 SPI harware support. The Pimoroni library has a PIO SPI driver, which gets around the problem.

## Screen shots
<img src="docs/screenshots/48k_boot_screen.png" height="200px"/> <img src="docs/screenshots/128k_boot_screen.png" height="200px"/> <img src="docs/screenshots/the_swarm_is_coming_1.png" height="200px"/> <img src="docs/screenshots/the_swarm_is_coming_2.png" height="200px"/> <img src="docs/screenshots/the_goblin_1.png" height="200px"/> <img src="docs/screenshots/the_goblin_2.png" height="200px"/> <img src="docs/screenshots/menu_main_vol.png" height="200px"/>

## Audio samples
* [The Swarm - 4 pin PWM](docs/audio/the_swarm_pwm_4pin.mp3)
* [The Goblin - 4 pin PWM](docs/audio/the_goblin_pwm_4pin.mp3)

## Firmware targets
Pre-built binary targets can be copied directly to a Pico Pi. 
They can be downloaded from the links in the table below or found in the uf2 folder.

Before attempting to update the firmware on your Pico make sure power supplies and any USB host devices have been disconnected (hub, keyboard, joysticks, etc.).

Push and hold the BOOTSEL button and plug your Pico into the USB port of your computer. Release the BOOTSEL button after your Pico is connected. It will mount as a Mass Storage Device called RPI-RP2. Drag and drop the UF2 file onto the RPI-RP2 volume.

<img src="docs/pico-bootsel.png" />

On hardware with a faceplate the button is usually accessible through a small hole; the PICOZX Lcd board has the Pico facing inwards and you will need to reach a finger inside to press the bootsel button.

| Board | Binary |
| ------ | -------- |
| [HDMI breadboard](docs/ZxSpectrumBreadboardHdmiNPinAudio.md) | [ZxSpectrumBreadboardHdmi1PinAudio.uf2](uf2/ZxSpectrumBreadboardHdmi1PinAudio.uf2) |
| [HDMI breadboard](docs/ZxSpectrumBreadboardHdmiNPinAudio.md) | [ZxSpectrumBreadboardHdmi2PinAudio.uf2](uf2/ZxSpectrumBreadboardHdmi2PinAudio.uf2) |
| [HDMI breadboard](docs/ZxSpectrumBreadboardHdmiNPinAudio.md) | [ZxSpectrumBreadboardHdmi4PinAudio.uf2](uf2/ZxSpectrumBreadboardHdmi4PinAudio.uf2) |
| [VGA breadboard](docs/ZxSpectrum4PinAudioVga1111Ps2.md) | [ZxSpectrum4PinAudioVga1111Ps2.uf2](uf2/ZxSpectrum4PinAudioVga1111Ps2.uf2) | 
| [PICO ZX48/128](docs/pico_zx48_128.md) | [ZxSpectrumPicomputerVgaAukBob.uf2](uf2/ZxSpectrumPicomputerVgaAukBob.uf2) |
| [PICOZX LCD](docs/ZxSpectrumPicomputerZxLcd.md)| [ZxSpectrumPicomputerZxLcd.uf2](uf2/ZxSpectrumPicomputerZxLcd.uf2) |
| [PICOZX LCD with negative LCD](docs/ZxSpectrumPicomputerZxLcd.md) | [ZxSpectrumPicomputerZxInverseLcd.uf2](uf2/ZxSpectrumPicomputerZxInverseLcd.uf2) |
| [PICO ZX LCD for ILI9341](docs/ZxSpectrumPicomputerZxLcd.md) | [ZxSpectrumPicomputerZxILI9341Lcd.uf2](/uf2/ZxSpectrumPicomputerZxILI9341Lcd.uf2) |
| [PICOZX](docs/ZxSpectrumPicomputerVga222Zx.md) | [ZxSpectrumPicomputerVga222Zx.uf2](uf2/ZxSpectrumPicomputerVga222Zx.uf2) |
| [RetroVGA](docs/ZxSpectrumPicomputerVga.md) | [ZxSpectrumPicocomputerVga.uf2](uf2/ZxSpectrumPicocomputerVga.uf2) |
| [PicomputerMax](docs/ZxSpectrumPicomputerMax.md) | [ZxSpectrumPicocomputerMax.uf2](uf2/ZxSpectrumPicocomputerMax.uf2) |
| [PicomputerZX](docs/ZxSpectrumPicomputerZX.md) | [ZxSpectrumPicocomputerZX.uf2](uf2/ZxSpectrumPicocomputerZX.uf2) |
| [Pimoroni Pico DV](docs/ZxSpectrumPicoDv.md) | [ZxSpectrumPicoDv.uf2](uf2/ZxSpectrumPicoDv.uf2) |
| [Pimoroni Pico VGA](docs/ZxSpectrumPicoVga.md) | [ZxSpectrumPicoVga.uf2](uf2/ZxSpectrumPicoVga.uf2) |
| [HDMI + key matrix](docs/ZxSpectrumBreadboardHdmiKbd1PinAudio.md) |  [ZxSpectrumBreadboardHdmiKbd1PinAudio.uf2](uf2/ZxSpectrumBreadboardHdmiKbd1PinAudio.uf2) |
| [ArnoldUK](docs/ZxSpectrumPicomputerVgaAuk.md) | [ZxSpectrumPicomputerVgaAuk.uf2](uf2/ZxSpectrumPicomputerVgaAuk.uf2) |
| [HDMI MURMULATOR](docs/MURMULATOR.md) | [ZX-MURMULATOR_HDMI.uf2](uf2/ZX-MURMULATOR_HDMI.uf2) |
| [VGA MURMULATOR](docs/MURMULATOR.md) | [ZX-MURMULATOR_VGA.uf2](uf2/ZX-MURMULATOR_VGA.uf2) |

e.g. for the HDMI breadboard wiring show above use:
```sh
cp ZxSpectrumBreadboardHdmi4PinAudio.uf2 /media/pi/RPI-RP2/
```


## Audio pins
There are two techniques for audio output. 
The first is a mixture of digital sound and PWM output, which comes in three variants.
The second is is using a DAC connected to the Pico using I2S.

### PWM/Digital Audio
PWM audio output comes in 3 variants 1, 2 and 4 pin:

| Label     | 1 Pin                  | 2 Pin               | 4 Pin                   |
| ----      | ---------------------- | ------------------- | ----------------------- |
| RP AUDIO1 | Buzzer & AY-3-8912 PWM | AY-3-8912 PWM       | AY-3-8912 Channel A PWM |
| RP AUDIO2  | -                      | Buzzer             | Buzzer                  |
| RP AUDIO3  | -                      | -                  | AY-3-8912 Channel B PWM |
| RP AUDIO4  | -                      | -                  | AY-3-8912 Channel C PWM |

High frequencies need to be filtered out of the PWM audio output and mixed with the Spectrum's digital audio.
Here are some sample designs. Please note they are not carefully designed but made from components I found lying around. 
If you create a particularly nice sounding design please let me know and I will add it to the documentation.

Separating out the Spectrum buzzer from the AY-3-8912 improves the fidelity of the Spectrum beeps.

![image](docs/Pico%202%20pin%20PWM%20audio%20filter%20mono.png)

The best audio is achieved by having separate pins for the Spectrum buzzer and AY-3-8912 A,B & C channels.

![image](docs/Pico%204%20pin%20PWM%20audio%20filter%20mono.png)

The sound is actually quite good from the 4 pin filter and at some point I will do a stero version. 

Designs that only have a single GPIO pin available can have the audio mixed digitally:

![image](docs/Pico%201%20pin%20PWM%20audio%20filter%20mono.png)

### I2S DAC Audio
The emulation can drive a PCM5100A DAC for line out audio over I2S.
It uses the RP_DAC_DATA, RP_DAC_BCLK and RP_DAC_LRCLK pin on the Pico.
Currently, only tested on the Pimoroni Pico DV board.

### Video output

#### DVI/HDMI
The following circuit shows roughly how to connect an HDMI socket; 
I have always used a breakout board... 

<a href="https://buyzero.de/products/raspberry-pi-pico-dvi-sock-videoausgabe-fur-den-pico">
<img src="https://cdn.shopify.com/s/files/1/1560/1473/products/Raspberry-Pi-Pico-Video-Output-DVI-Sock-topview_1200x.jpg" width="200"/>
</a>

<a href="https://thepihut.com/products/adafruit-dvi-breakout-board-for-hdmi-source-devices">
<img src="https://cdn.shopify.com/s/files/1/0176/3274/products/adafruit-dvi-breakout-board-for-hdmi-source-devices-adafruit-ada4984-28814829158595_600x.jpg" width="200"/>
</a>

...but this is what I think it boils down to:

![image](docs/Pico%20DVI%20over%20HDMI.png)

So far, there are three supported VGA configurations, which can be found in the various build targets.
They have all been designed with a combination of plagiarism and guesswork,
so please let me know if you have better versions and I will update this document.
#### VGA RGBY 1111
Although this is the most complicated, it is my favourite as it only uses 5 pins on the Pico. The display is slightly paler than the other two versions, which is easier on the eyes.

![image](docs/Pico%20VGA%20RGBY1111.png)

See this [CMakeLists.txt](src/vga/CMakeLists.txt) for an example configuration.
#### VGA RGB 222

![image](docs/Pico%20VGA%20RGB222.png)

See this [CMakeLists.txt](src/picomputer/picomputer_vga_zx/CMakeLists.txt) for an example configuration.
#### VGA RGB 332

![image](docs/Pico%20VGA%20RGB332.png)

See this [CMakeLists.txt](src/picomputer/picomputer_vga/CMakeLists.txt) for an example configuration.

### PS/2 Keyboards
The emulator targets can accept input from a PS/2 keyboard wired to RP_PS2_DATA and RP_PS2_CLK.
A suggested circuit is shown below:

![image](docs/Pico%20PS2%20interface.png)

The resistors and Zeners are there in case the keyboard contains a pull-up resistor to 5v on either the data or clock lines;
the data and clock lines are, in theory, open-collector with no pull-up.

I'm told most PS/2 keyboards can be run at 3.3v and the the extra components become redundant... but I've not tried with mine. 
You may find the Pico struggles to deliver enough power at 3.3v for the SD card writes and running a keyboard.

Currently there is no toggling on the lock keys (caps/num lock) and the indicator leds are not used.

### Audio Input

Due to a great deal of help from [badrianiulian](https://github.com/badrianiulian), here is a suggested audio input circuit:

![image](docs/badrianiulian_audio_1.jpg)

Suggestions to improve this circuit are appreciated and please post them [here](https://github.com/fruit-bat/pico-zxspectrum/issues/46).

## Components 
<a href="https://shop.pimoroni.com/products/raspberry-pi-pico">
<img src="https://cdn.shopify.com/s/files/1/0174/1800/products/PICOBOARDWHITEANGLE2_768x768.jpg" width="200"/>
</a>

<a href="https://buyzero.de/products/raspberry-pi-pico-dvi-sock-videoausgabe-fur-den-pico">
<img src="https://cdn.shopify.com/s/files/1/1560/1473/products/Raspberry-Pi-Pico-Video-Output-DVI-Sock-topview_1200x.jpg" width="200"/>
</a>

<a href="https://thepihut.com/products/adafruit-dvi-breakout-board-for-hdmi-source-devices">
<img src="https://cdn.shopify.com/s/files/1/0176/3274/products/adafruit-dvi-breakout-board-for-hdmi-source-devices-adafruit-ada4984-28814829158595_600x.jpg" width="200"/>
</a>

<a href="https://thepihut.com/products/adafruit-micro-sd-spi-or-sdio-card-breakout-board-3v-only">
<img src="https://cdn.shopify.com/s/files/1/0176/3274/products/adafruit-micro-sd-spi-or-sdio-card-breakout-board-3v-only-adafruit-ada4682-28609441169603_600x.jpg" width="200"/>
</a>

<a href="https://shop.pimoroni.com/products/adafruit-stemma-speaker-plug-and-play-audio-amplifier">
<img src="https://cdn.shopify.com/s/files/1/0174/1800/products/3885-02_630x630.jpg" width="200"/>
</a>


### Pico pinout

![image](docs/Pico-R3-SDK11-Pinout.svg "Pinout")


## Issues
The Z80 is interrupted at the end of each frame at 60hz. The original Spectrum wrote frames at 50hz, so some code runs more frequently than it used to; there is a 4Mhz CPU setting that kind of balances this up.

There is now preliminary support for Kempston & Sinclair joysticks.

A USB hub can be connected to the RP2040 allowing a keyboard and joysticks to be used with the Spectrum. The code is a bit new and I don't know how many different joysticks will be supported; if you are having trouble raise an issue and attach a HID report descriptor from your device and I will have a look at it.

To get this to work I have done some hacking and slashing in [TinyUSB](https://github.com/hathach/tinyusb) (sorry Ha Thach): 

https://github.com/fruit-bat/tinyusb/tree/hid_micro_parser

## Build
The version of [TinyUSB](https://github.com/hathach/tinyusb) in the [Pico SDK](https://github.com/raspberrypi/pico-sdk)
will need to be replaced with a version containing a HID report parser and USB hub support.

Using *git* protocol:
```sh
cd $PICO_SDK_PATH/lib/
mv tinyusb tinyusb.orig
git clone git@github.com:fruit-bat/tinyusb.git
cd tinyusb
git checkout hid_micro_parser
```
...or using *https* protocol:
```sh
cd $PICO_SDK_PATH/lib/
mv tinyusb tinyusb.orig
git clone https://github.com/fruit-bat/tinyusb.git
cd tinyusb
git checkout hid_micro_parser
```

Make a folder in which to clone the required projects e.g.
```sh
mkdir ~/pico
cd ~/pico
```

Clone the projects from github:

Using *git* protocol:
```sh
git clone git@github.com:raspberrypi/pico-extras.git
git clone git@github.com:Wren6991/PicoDVI.git
git clone git@github.com:fruit-bat/pico-vga-332.git
git clone git@github.com:fruit-bat/pico-zxspectrum.git
git clone git@github.com:pimoroni/pimoroni-pico.git
git clone git@github.com:fruit-bat/pico-dvi-menu
git clone git@github.com:fruit-bat/pico-emu-utils
git clone git@github.com:redcode/Z80.git
git clone git@github.com:redcode/Zeta.git
```
...or using *https* protocol:
```sh
git clone https://github.com/raspberrypi/pico-extras.git
git clone https://github.com/Wren6991/PicoDVI.git
git clone https://github.com/fruit-bat/pico-vga-332.git
git clone https://github.com/fruit-bat/pico-zxspectrum.git
git clone https://github.com/pimoroni/pimoroni-pico.git
git clone https://github.com/fruit-bat/pico-dvi-menu
git clone https://github.com/fruit-bat/pico-emu-utils
git clone https://github.com/redcode/Z80.git
git clone https://github.com/redcode/Zeta.git
```
Edit:
```sh
pimoroni-pico/drivers/fatfs/ffconf.h
```
and set FF_USE_FIND to 1
```
#define FF_USE_FIND            1
```


Perform the build:
```sh
cd pico-zxspectrum
mkdir build
cd build
cmake -DPICO_COPY_TO_RAM=0 ..
make clean
make -j4
```

Building for the *Pimoroni Pico VGA Demo Base* needs a different cmake command:

```sh
cd build
cmake -DPICO_COPY_TO_RAM=0 -DPICO_BOARD=vgaboard ..
make -j4 ZxSpectrumPicoVga
```

Copy the relevant version to your board, which can be located with:
```sh
find . -name '*.uf2'
```
e.g.
```sh
cp ./bin/breadboard_hdmi/ZxSpectrumBreadboardHdmi.uf2 /media/pi/RPI-RP2/
```

## Prepare an SD card
The following table shows the folders used by the emulator on the SD card.
If not already present, they will be created as the emulator starts up.

| Folder | Contents |
| ------ | -------- |
| zxspectrum/snapshots | Put your .z80 snapshot files in here. |
| zxspectrum/snapshots/quicksaves | Folder for quick saves. |
| zxspectrum/tapes | Folder for .tap and .tzx tape files. |

## USB and PS2 Keyboard mappings

| Key | Action |
| --- | ------ |
| AltGr | Symbol |
| F1 | Toggle on screen menu |
| F3 | Toggle mute |
| F4 | Toggle the Z80 moderator. Cycles through 3.5Mhz, 4.0Mhz and unmoderated |
| F8 | Reload current snap |
| F9 | previous snap |
| F10 | next snap |
| F11 | Reset as 48k Spectrum |
| F12 | Reset as 128k Spectrum |
| LCtrl + F1-F12 | Quick save (LCtrl+F1 = save slot 1, LCtrl+F2 = save slot 2, etc) |
| LAlt + F1-F12 | Quick load (LAlt+F1 = load slot 1, LAlt+F2 = load slot 2, etc) |

## Debug
<a href="https://shop.pimoroni.com/products/usb-to-uart-serial-console-cable">
<img src="https://cdn.shopify.com/s/files/1/0174/1800/products/USB_UART_1_of_2_630x630.JPG" width="200"/>
</a>

| Pico pin | Pico GPIO | Adapter wire |
| -------- | --------- | ------------ |
| 1        | GP0       | White        |
| 2        | GP1       | Green        |
| 3        | GND       | Black        |

```sh
tio -m ODELBS /dev/ttyUSB0
```
## Thanks to
[CarlK](https://github.com/carlk3/) for the super [no OS FAT FS for Pico](https://github.com/carlk3/no-OS-FatFS-SD-SPI-RPi-Pico)<br/>
[Damien G](https://damieng.com/) for maintaining and publishing some wonderful [8-bit fonts](https://damieng.com/typography/zx-origins/)<br/>
[Wren](https://github.com/Wren6991/) for the amazing [PicoDVI](https://github.com/Wren6991/PicoDVI)<br/>
[hathach](https://github.com/hathach) for the embeded USB library [TinyUSB](https://github.com/hathach/tinyusb)<br/>
[Lin Ke-Fong](https://github.com/anotherlin) for the [Z80 emulator](https://github.com/anotherlin/z80emu)<br/>
[Pimoroni](https://github.com/pimoroni/pimoroni-pico) for lots of useful libraries</br>
[badrianiulian](https://github.com/badrianiulian) for help testing and design work on the audio circuitry<br/>
[redcode](https://github.com/redcode/Z80) for the [Z80 emulator](https://github.com/redcode/Z80)<br/>
[Javavi](https://github.com/javavi) for adding support for the MURMULATOR platform <br/>

## References
[Z80 Test suite](https://github.com/raxoft/z80test)<br/>
[Wren's Amazing PicoDVI](https://github.com/Wren6991/PicoDVI)<br/>
[Z80 file format documentation](https://worldofspectrum.org/faq/reference/z80format.htm)<br/>
[Fonts by DamienG](https://damieng.com/typography/zx-origins/)<br/>
[breakintoprogram - Screen memory layout](http://www.breakintoprogram.co.uk/computers/zx-spectrum/screen-memory-layout)<br/>
[breakintoprogram - keyboard layout](http://www.breakintoprogram.co.uk/computers/zx-spectrum/keyboard)<br/>
[breakintoprogram - interrupts](http://www.breakintoprogram.co.uk/computers/zx-spectrum/interrupts)<br/>
[worldofspectrum - 48k ZX Spectrum reference](https://worldofspectrum.org/faq/reference/48kreference.htm)<br/>
[worldofspectrum - 128k ZX Spectrum reference](https://worldofspectrum.org/faq/reference/128kreference.htm)<br/>
[worldofspectrum - AY-3-8912 reference](https://worldofspectrum.org/ZXSpectrum128Manual/sp128p13.html)<br/>
[JGH Spectrum ROM](http://mdfs.net/Software/Spectrum/Harston/)<br/>
[48k ZX Spectrum service manual](https://www.1000bit.it/support/manuali/sinclair/zxspectrum/sm/section1.html)<br/>
[GOSH ZX Spectrum ROM](https://k1.spdns.de/Vintage/Sinclair/82/Sinclair%20ZX%20Spectrum/ROMs/gw03%20'gosh%2C%20wonderful'%20(Geoff%20Wearmouth)/gw03%20info.htm)<br/>
[Cassette input circuit design](http://www.zxdesign.info/cassette.shtml)<br/>
[ZX Spectrum ROM Images](https://mdfs.net/Software/Spectrum/ROMImages/)<br/>
[AY-3-8912 - manual](https://cpctech.cpc-live.com/docs/ay38912/psgspec.htm)<br/>
[AY-3-8912 - synth](http://www.armory.com/~rstevew/Public/SoundSynth/Novelty/AY3-8910/start.html)<br/>
[USB HID 1.1](https://www.usb.org/sites/default/files/hid1_11.pdf)<br/>
[ST7789 LCD driver reference](docs/ST7789_Datasheet.pdf)<br/>
[RGB for 128k ZX Spectrum](docs/128_rgb.pdf)<br/>
[PS/2 vs HID keyboard codes](docs/ps2-hid.pdf)<br/>
[PCM 5100A DAC](PCM510xA.pdf)<br/>
[RP2040 Datasheet](https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf)</br>
[Z80 Instruction set with XYH](https://wikiti.brandonw.net/?title=Z80_Instruction_Set)</br>
[Z80 Instruction set](https://clrhome.org/table/)</br>
[Site with some WAV files](http://zx.zigg.net/zxsoftware/)</br>
[ZX Modules Software](https://spectrumforeveryone.com/technical/zx-modules-software/)</br>
[TZX format](https://www.alessandrogrussu.it/tapir/tzxform120.html#GRPSTART)</br>
[A decoder for ZX format](https://github.com/kounch/playtzx)</br>
[Circuit diagram editor](https://www.circuit-diagram.org/)</br>

