ESPHome Power Meter
====================

Yet another version of a non-invasive Power Meter for use in [Home Assistant](https://www.home-assistant.io/), using the [Pulse Meter](https://esphome.io/components/sensor/pulse_meter.html) component in [ESPHome](https://esphome.io/).

I've used [Home Assistant Glow](https://github.com/klaasnicolaas/home-assistant-glow) for a while without problems. I decided that it would be cool to also have hourly totals and be able to track costs as well, without having to rely on Rieman Integrals, Utility Meters and such in HA. 

Note: Because of how ESPHome does things, I had to implement several work-arounds, and should probably convert this whole thing to a custom component in ESPHome. However this - although far from elegant - actually seems to work.

The kWh price is imported as a sensor from Home Assistant, using the [Nordpool Custom Component](https://github.com/custom-components/nordpool), but can also be set 'manually' with a Number component in HA. Ideally the price should be fetched directly from NordPool using their API, but I haven't looked at that yet.

To test the accuracy of the Power Meter, I created a simple Arduino Sketch to simulate the flashing led on a 'real' Power Meter. A led blinking at specific intervals to simulate power consumption. You'll find it [here](https://github.com/zenzay/arduino-projects/tree/main/power-meter-pulse-led). I also disabled the kWh Price sensor import from HA, so the price stayed fixed during testing.

*Please bear in mind that this is work in progress and a lot of the code is quite kludgy.*

Note: You can find an extended version with RTC and E-Ink Display [here](../power-meter-2/).

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

