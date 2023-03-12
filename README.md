ESPHome Power Meter
====================

## A Release version is not quite ready yet. A few bugs to get rid off first. ##


### Yet another- version of a non-invasive Power Meter for use in [Home Assistant](https://www.home-assistant.io/), using the [Pulse Meter](https://esphome.io/components/sensor/pulse_meter.html) component in [ESPHome](https://esphome.io/). ###

I've used [Home Assistant Glow](https://github.com/klaasnicolaas/home-assistant-glow) for a while without problems. I decided that it would be cool to also have the ESP track costs as well. That way I could do away with Rieman Sum and Utility Meter integrations in HA. 

Note: Because of how ESPHome does things, I had to implement several work-arounds, and should probably convert this whole thing to a custom component in ESPHome. However this - although far from elegant - actually seems to work.

The kWh price is imported as a sensor from Home Assistant, using the [Nordpool Custom Component](https://github.com/custom-components/nordpool), but the price can also be set 'manually' with a Number component. Ideally the price should be fetched directly from NordPool using their API.

To test the accuracy of the Power Meter, I created a simple Arduino Sketch to simulate the blinking LED on a 'real' Power Meter. A simple LED blinking at specific intervals to simulate power consumption. You'll find it [here](https://github.com/zenzay/arduino-projects/tree/main/power-meter-pulse-led). I also disabled the kWh Price sensor import from HA, temporarily in the code, so the price stayed fixed during testing.

*Please bear in mind that this hasn't been tested extensively and I take absolutely no responsibility for any suprisingly large electricity bills*

Components
-----------

* Wemos D1 Mini ESP32 (any ESP32 will do. An ESP8266 *should* work too, but it's not as fast and has fewer pins)
* LM393 Photodiode Sensor module


Wiring
-------

[LM393 Photodiode Sensor module](https://www.mysensors.org/build/light-lm393)
| BOARD PIN | ESP32 PIN |
|----------:|-----------|
|       D0  |       26  |
|       A0  |       NC  |
|      VCC  |      VCC  |
|      GND  |      GND  |

