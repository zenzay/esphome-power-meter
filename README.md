ESPHome Power Meter w/ E-Ink Display
====================================

## Not ready for release ##

#### Status Page ####
![pm_page_1](./assets/pm-page-1.jpg)
#### Daily Usage Graph ####
![pm_page_2](./assets/pm-page-2.jpg)
#### Daily Cost Graph ####
![pm_page_3](./assets/pm-page-3.jpg)

This is the 'extended' version of my ESPHome Power Meter. This version adds an E-Ink Display and a humble push button. The button enables turning pages on the display manually. Main page is a - sort of - status page and the subsequent pages shows some graphs and stuff.  To make it easier for myself - not wanting to draw every single line on the display - I've created some transparent backgrounds in GIMP, and just pop those on the display before drawing the rest.

Note 1: The display code is quite messy and really should be rewritten.

Note 2: Put the pictures from the images folder in the ESPHome folder before installing.

Note 3: Achieving transparency when drawing images on displays in ESPHome can be tricky. I often ended up with exporting PNGs from GIMP that, to the naked eye, looked like they were fully transparent, but they were apparently not 100% and turned up black on the display. What seemed to fix it was to fill all areas, that I wanted transparent, with white and subsequently Magic Select the areas and delete them.


Components
-----------

* Wemos D1 Mini ESP32. Any ESP32 should work. An ESP8266 *might* work, but you'll have fewer pins available.
* [LM393 Photodiode Sensor module](https://www.mysensors.org/build/light-lm393)
* [Waveshare 2.9" E-Ink Display](https://www.waveshare.com/2.9inch-e-paper-module.htm)
* [Push Button](https://www.switchelectronics.co.uk/black-microminiature-5mm-momentary-off-on-push-button-spst-0-5a)

Wiring
-------

#### Waveshare E-Ink Display ####
| DISPLAY | ESP32 |
|--------:|-------|
|   BUSY  |   19  |
|    RST  |   16  |
|    DC   |   17  |
|    CS   |    5  |
|   CLK   |   18  |
|   DIN   |   23  |
|   GND   |  GND  |
|   VCC   |  3.3v |

#### LM393 Photodiode Module ####
| MODULE | ESP32 |
|-------:|-------|
|    D0  |   26  |
|    A0  |   NC  |
|   VCC  |  VCC  |
|   GND  |  GND  |

#### Push Button ####
|  PIN | ESP32 |
|-----:|-------|
|   1  |  GND  |
|   2  |   25  |
