# ESP32 D1 Mini D1 RGB Matrix Shield 

This shield is the following of this [project](https://github.com/hallard/WeMos-Matrix-Shield) but I created a new repo since the board is different, wiring also and even the library used to drive Matrix.

This board is used to simplify ESP32 connectivity with a nice matric RGB led. This idea came from excellent project called [Morphing Digital Clock][3] done by [HariFun][1] Instructable. But with this library and current code I got some issues with mutitasking, and using same time the awesome Async libraries ([Web Server](https://github.com/me-no-dev/ESPAsyncWebServer) and [MQTT](https://github.com/marvinroger/async-mqtt-client)) getting very ofther in reboot and board reset. I don't blame anyone, the library used was just to drive matrix, it's always complicated mixing some libraries sometimes especially ones with hardware intensive related suff, IRQ's and TCP.

This was until [@mrfaptastic](https://github.com/mrfaptastic/ESP32-HUB75-MatrixPanel-I2S-DMA) released the DMA version wich is far less CPU intensive. I tested this one with Async Web Server, Async MQTT and OTA without any issue. You can participate to the @vortigont started discussion [here](https://github.com/mrfaptastic/ESP32-HUB75-MatrixPanel-I2S-DMA/discussions/96) Thanks to github for this new feature.


See it in action, nice isn't it?

<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/WeMos-Matrix-Shield-DMA.gif">

This breakout has just few minimal features.

**New in Version V1.9**

- Touchpad 9 (T9) used and wired to GPIO32
- Exposed (top right corner) GPIO0 instead of GPIO32
- Reversed I2C connector order, because all I2C wiring have components on top except Luminosity TSL2561 BH1750, now fixed
- I2C connector order have drilled holes to match sensor plug, no need to solder to fix or swap sensor type. Just press it to fit into holes
- Added another pin close to I2C connector connected to GPIO34 (for using sensor IRQ pin for example)
- Major re-routing to fix issues


**New in Version V1.8a**

- **this PCB version does not work, please don't use it**
- Added C1, C2, C3 footprints. It's to add capacitor to poor 3.3V VOut of esp32 on board regulator. This one is not output filtered enough resulting sometimes with brownout reset loop. Now you can plug radial or 1 (or 2) SMD 0805 in parallel

**New in DMA Version V1.8**

- **this PCB version does not work, please don't use it**
- Removed ESP8266 compatibility, since DMA need more GPIO it's now exclusive to ESP32 boards with WeMos Mini D1 wiring called ESP32 Mini Kit or ESP32 Wemos, or ESP32 MH-ET Live such as this [banggood model](https://www.banggood.com/Wemos-D1-Mini-ESP32-ESP-32-WiFiBluetooth-Internet-Of-Things-Development-Board-Based-ESP8266-p-1205854.html) or this [aliexpress](https://www.aliexpress.com/item/MH-ET-LIVE-D1-mini-ESP32-ESP-32-WiFi-Bluetooth-Internet-of-Things-development-board-based/32815530502.html). But you can find a lot also on ebay, not a problem.
- PCB board has been extented to fit this ESP32 Mini module .
- LDR to dynamically change brightness according to ambiant light
- I2C connectors as header and Groove to plug a bunch of sensors
- Added one touch pad button
- No need to wire back the shield to HUB75 output of the Matrix Panel


Please check wiring and picture before ordering, should looks like something like that:

<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/esp32-mini-all.jpg">

<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/esp32-mini.jpg">

**V1.9 are fully tested and working**.

**V1.8 and V1.8a boards are not working** I've been too confident, this is the 1st time I need to throw out all boards. Reason is that both ESP32 headers the ones side by side were reversed (on each side).
I mean the 1st was the 2nd and vice versa), So as you can imagine nothing was unable to works, even flashing ESP32.

# Detailed Description

Look at the schematics for more informations.

# Schematic  

<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/WeMos-Matrix-Shield-DMA-sch.png">

# Boards  

<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/WeMos-Matrix-Shield-DMA-top.png" alt="Top" width="45%" height="45%">&nbsp;
<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/WeMos-Matrix-Shield-DMA-bot.png" alt="Bottom" width="45%" height="45%">

~~You can order PCBs of this board at [PCBs.io)(ttps://www.pcbs.io/)~~

 ~~PCBs.io give me some reward when you order my designed boards from their site. This is pretty good, because I can use these rewards to create and design new boards and order boards for a discounted price, so if you don't care about PCB manufacturer please use PCBs.io.~~

Looks like PCBs.io is gone, I do not have any rewards from PCBs.io since August 2020 and my free order placed after are still not received, so my guess they are not on business anymore and my $1000 rewards are not usable anymore, too bad.

So you can order the board on [oshpark](https://oshpark.com) or submit gerbers.zip file to any PCB manufacturer of your choice.

- [V1.9](https://oshpark.com/shared_projects/gCeBFgxd)

It's a pitty after several discuss with OSHPark that I can't have any rewards for each people ordering my boards, this would allow me to order free PCB for shared projects and create new ones. For information my shared boards generated a total of **$285 162.00** orders at PCBs.io in 4 years, not bad at all :-)

Hoping one day OSHparks will thanks me giving them this market. 

# Firmware

I suggest you to look at the awesome [examples](https://github.com/mrfaptastic/ESP32-HUB75-MatrixPanel-I2S-DMA/tree/master/examplesk) located in the [library](https://github.com/mrfaptastic/ESP32-HUB75-MatrixPanel-I2S-DMA) driving the Matrix Panel.
 
# Assembled boards

<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/WeMos-Matrix-Shield-DMA-assembled-top.jpg" alt="Assembled Top" width="45%" height="45%">&nbsp;
<img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/WeMos-Matrix-Shield-DMA-assembled-bot.jpg" alt="Assembled Bottom" width="45%" height="45%">

# BOM

Nothing fancy, just some headers and 2 differents power conector (choose the one you prefer) :

 - 10K 0805 resistor for LDR
 - Any LDR PhotoCell 5528
 - I2C 4.7K resistor 0805 if needed, default I2C set to 3.3V use JP3 if you prefer 5V
 - For better stability C1 100uF 16V electrolytic, or C2 100uF 0805, or C2+C3 47uF 0805
 - Diode can be any Schottky diode barrier and is not mandatory (if not close JP4 jumper)
 - Ebay search for "DC Power Jack Barrel PCB Mount"
 - 7.62mm barrier terminal block [example](https://ebyelectro.com/terminal-block-product-info.asp?ProductID=333)
 - Ebay search for "2X8 Pin 2.54mm Double Row Female Header" or polulu product #1028, you can also use twice 1x8 pin female or even twice 2x4 pins female, plenty of option for this one
 
 <img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/DC-Power-Barrel.jpg">
 <img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/barrier-7_62.png">
 <img src="https://github.com/hallard/WeMos-Matrix-Shield-DMA/blob/main/pictures/2X8-pin-connector.jpg">

# License

<img alt="Creative Commons Attribution-NonCommercial 4.0" src="https://i.creativecommons.org/l/by-nc/4.0/88x31.png">   

This work is licensed under a [Creative Commons Attribution-NonCommercial 4.0 International License](http://creativecommons.org/licenses/by-nc/4.0/)    

# Misc

See news and other projects on my [blog][2] 

Thanks to @mrfaptastic, @vortigont, @me-no-dev and all other I may forgot.
 
[1]: https://www.instructables.com/member/HariFun/
[2]: https://hallard.me
[3]: https://www.instructables.com/id/Morphing-Digital-Clock/
[4]: https://PCBs.io/share/

[20]: https://wiki.wemos.cc/products:d1:d1_mini_lite
[21]: https://wiki.wemos.cc/products:d1:d1_mini
[22]: https://wiki.wemos.cc/products:d1:d1_mini_pro