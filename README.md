# TOHKBD rev2

## History

When Jolla announced their [Jolla phone](https://www.youtube.com/watch?v=tRZxM9rNyZ4) the mobile Linux community rejoiced and finally had a place to go from their N8x, N900, N950 or N9. Together with the new operating system on the inside, the OtherHalf concept was introduced. With direct data-connection into the phone it is now possible to extend the functionality on a hardware level.

Naturally, a keyboard OtherHalf was the [most requested feature](http://www.jollatides.com/2013/10/03/other-half-lets-prioritise/) by the community by far. Jolla however was still getting started and getting their phone launched with the minimum of Sailors at the time. This was left to the community to develop.

In [June 2013](http://talk.maemo.org/showthread.php?t=91535) one idiot thought he could easily make this -how hard could it be, really?- and started on his journey. After some time this foolish individual make TOHKBD-rev1: hackish, ugly, frankensteined, terrible durability and way too much work to assemble. But it worked. 

After this project ended there was a period of other Funky-TOH development, with during that time a lot of requests of making more keyboards. Little did they knew that in the background the imfamous 'dirkvl' together with his trusty 'kimmoli' were cooking up a new version. A better one. The One.

With an [open application](https://twitter.com/andrewzhilin/status/493485714798313472) on the hashweb/tweetspace Andrew joined the team and provid himself to be the missing piece of the three piece puzzle. With a complete team, a solid design and a strong backing from the rest of the community, the TOHKBD-team set out onto the open crowdfunding see. [And struck gold.](https://www.kickstarter.com/projects/2028347278/tohkbd-the-other-half-keyboard-for-your-jolla)

## Hardware

### Electronics

#### TOH-cover

In the cover that snap onto the phone there is very little going on. There is a PCB that connects to all [6 pogo-pins](https://jolla.com/the-other-half-developer-kit/). Connecting to these pins is a [voltage regulator](https://github.com/dirkvl/TOHKBD/tree/master/Eagle/pics/MCP1703.jpg) and an EEPROM. 

![EEPROM](https://github.com/dirkvl/TOHKBD/tree/master/Eagle/pics/EEPROM.jpg)

This is a memory module that contains a [Vendor and Product ID](https://wiki.merproject.org/wiki/The_other_half). The phone reads this EEPROM when it connects to start the appropriate driver.

If the driver is not installed, the phone reads the [NFC tag](http://www.nfcnetstore.com/SMARTRAC+Midas+NTAG203+12x19+mm+clear+%28NFC+Forum+Type+2%29/p/121/) on the PCB and pulls the driver from the store.

With two contact pads (8mm PCBs) the keyboard piece can make contact, all 6 pins are available.

#### Keyboard piece

In the keyboard a little more is going on. The main driver is the [TCA8424](http://www.ti.com/product/TCA8424/description).

![TCA8424](https://github.com/dirkvl/TOHKBD/tree/master/Eagle/pics/TCA8424.jpg)

This connects to the keyboard matrix. It waits untill a key is pressed, then starts scanning and notifies the phone via the Interrupt pin that is has data to be read.

![Keyboard matrix](https://github.com/dirkvl/TOHKBD/tree/master/Eagle/pics/matrix.jpg)

There is an additional EEMPROM in the keyboard piece, containing the keypad layout version.

![Keyboard EEPROM](https://github.com/dirkvl/TOHKBD/tree/master/Eagle/pics/EEPROM2.jpg)

The backlight consists of 10 x 0402 LEDs, controlled with a [n-channel MOSFET](http://en.wikipedia.org/wiki/MOSFET) by the TCA8424.

![Backlight](https://github.com/dirkvl/TOHKBD/tree/master/Eagle/pics/backlight.jpg)

The keyboard detection is done with a PNP transistor.

![Backlight](https://github.com/dirkvl/TOHKBD/tree/master/Eagle/pics/detection.jpg)

```
1. Phone detects TOH-cover
2. Phone launches TOHKBD driver
3. The driver shuts down the 3V3 line and starts listening to the interrupt
4. When the keyboard connects, the PNP transistor shorts the interrupt line to ground
5. The phone detects the grounding of INT and powers up de 3V3 line
6. The 3V3 disables the grounding on INT in the transistor
7. The phone probes whether the TCA8424 is present
8a. If the TCA8424 is present, the keyboard is present and working and all is set in motion
8b. If the TCA8424 is not present, something is wrong and the phone goes back to step 3
```

SMD parts list:
```
To be made, but no surprises to be expected
```

### PCBs

From itead

### SMD assembly

P&P etc

### Frames

Info about 3d printing, to be made

### Magnet system

With locations etc

### Keypad

Credits to Andrew

### Layouts

designs, files etc

### Backplate

Dimensions

## Software

[Link to Kimmoli's Github](https://github.com/kimmoli/)
