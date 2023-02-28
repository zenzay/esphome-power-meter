ESPHome Power Meter w/ RTC and Display
======================================

This is the extended version of my [Power Meter](https://github.com/zenzay/esphome-projects/tree/main/power-meter). This version adds a RTC module and E-Ink Display

Yet another version of a non-invasive Power Meter for use in [Home Assistant](https://www.home-assistant.io/), using the [Pulse Meter](https://esphome.io/components/sensor/pulse_meter.html) component in [ESPHome](https://esphome.io/).

I've used [Home Assistant Glow](https://github.com/klaasnicolaas/home-assistant-glow) for a while without problems. I decided that it would be cool to also have hourly totals and be able to track costs as well, without having to rely on Rieman Integrals, Utility Meters and such in HA. 

Note: Because of how ESPHome does things, I had to implement several work-arounds, and should probably convert this whole thing to a custom component in ESPHome. However this - although far from elegant - actually seems to work.

The kWh price is imported as a sensor from Home Assistant, using the [Nordpool Custom Component](https://github.com/custom-components/nordpool), but can also be set 'manually' with a Number component in HA. Ideally the price should be fetched directly from NordPool using their API, but I haven't looked at that yet.

I've added a RTC Module in order to not miss time events (on the hour, midnight and so on). This way I can be reasonable sure to not miss anything when I'm fiddling with Home Assistant or my router is down. I probably shouldn't rely on Cron to track time events, but then again, this whole thing should probably be a custom component (but I repeat myself).

This version also adds a 2.9" E-Ink Display and a push button. The button anables turning pages on the display manually. Main page is a - sort of - status page and the subsequent pages shows some graphs and stuff.  To make it easier for myself - not wanting to draw every single line on the display - I've created some transparent backgrounds in GIMP, and just pop those on the display before drawing the rest.

Side note: Achieving transparency when drawing images on displays in ESPHome can be tricky. I often ended up with exporting PNGs from GIMP that, to the naked eye, looked like they were fully transparent, but they were apparently not 100% and turned up black on the display. What seemed to fix it was to fill all areas, that I wanted transparent, with white and subsequently Magic Select the areas and delete them.

To test the accuracy of the Power Meter, I created a simple Arduino Sketch to simulate the flashing led on a 'real' Power Meter. A led blinking at specific intervals to simulate power consumption. You'll find it [here](https://github.com/zenzay/arduino-projects/tree/main/power-meter-pulse-led). I also disabled the kWh Price sensor import from HA, so the price stayed fixed during testing.

*Please bear in mind that this is work in progress and a lot of the code is quite kludgy.*


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
