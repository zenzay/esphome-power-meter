ESPHome Power Meter w/ RTC and Display
======================================

## Not ready for release ##

This is the extended version of my ESPHome Power Meter. This version adds a RTC module, an E-Ink Display and a humble push button.

The RTC module is definitely more precise than the onboard RTC, and by having it, we only need to sync with the other time source, HA or SNTP.

This version also adds a 2.9" E-Ink Display and a push button. The button enables turning pages on the display manually. Main page is a - sort of - status page and the subsequent pages shows some graphs and stuff.  To make it easier for myself - not wanting to draw every single line on the display - I've created some transparent backgrounds in GIMP, and just pop those on the display before drawing the rest.

Side note: Achieving transparency when drawing images on displays in ESPHome can be tricky. I often ended up with exporting PNGs from GIMP that, to the naked eye, looked like they were fully transparent, but they were apparently not 100% and turned up black on the display. What seemed to fix it was to fill all areas, that I wanted transparent, with white and subsequently Magic Select the areas and delete them.

Components
-----------

* Wemos D1 Mini ESP32 (any ESP32 will do. An ESP8266 *should* work too, but it's not as fast and has fewer pins)
* DS 3131 Real Time Clock Module (DS1307 also works)
* 2.9" E-Ink Display (Waveshare or other)
* Physical Push Button

Wiring
-------

[Waveshare 2.9" E-Ink Display](https://www.waveshare.com/2.9inch-e-paper-module.htm)
| BOARD PIN | ESP32 PIN |
|----------:|-----------|
|     BUSY  |       19  |
|      RST  |       16  |
|      DC   |       17  |
|      CS   |        5  |
|     CLK   |       18  |
|     DIN   |       23  |
|     GND   |      GND  |
|     VCC   |      3.3v |


[DS3231 I2C Real Time Clock Module](https://components101.com/modules/ds3231-rtc-module-pinout-circuit-datasheet)
| BOARD PIN | ESP32 PIN |
|----------:|-----------|
|      SDA  |       21  |
|      SCL  |       22  |
|      VCC  |      VCC  |
|      GND  |      GND  |

[LM393 Photodiode Sensor module](https://www.mysensors.org/build/light-lm393)
| BOARD PIN | ESP32 PIN |
|----------:|-----------|
|       D0  |       26  |
|       A0  |       NC  |
|      VCC  |      VCC  |
|      GND  |      GND  |

[Push Button](https://www.switchelectronics.co.uk/black-microminiature-5mm-momentary-off-on-push-button-spst-0-5a)
|  PIN | ESP32 PIN |
|-----:|-----------|
|   1  |      GND  |
|   2  |       27  |
