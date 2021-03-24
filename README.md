# SENTSOR Core ESP32-DEV
## Introduction
<img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-render2.png" width="600">  

Introducing a new SENTSOR Core Board ESP32-DEV: all-in-one, general purpose development board based on latest revision of ESP32 chip. As usual, SENTSOR Core Board comes with extremely accurate RTC and MicroSD slot, with additional features for built-in development like environment (temperature & humidity) sensor, addressable RGB LED, and USB to UART bridge! Yes, we heard you! We know it's not a big deal, but we haven't urge to add this chip to aim design simplicity and low power usage (rarely used function once deployed). But for development purpose, it's surely helpful to have onboard USB to UART bridge to ease firmware update or debugging.

This board is a revision from previous [SENTSOR Core Board WROOM-32U](https://github.com/adamalfath/sentsor-core-wroom32u) (R1.0) board. This revision also comes with two flavours, named ESP32-DEV (this one) aimed for general purpose development board, and [ESP32-EMBED](https://github.com/adamalfath/sentsor-core-esp32embed) aimed for super low power and battery powered development board for embedded application.

## Features
<img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-pinoutposter.png" width="600">  

- **Compact & powerful**, measured only 58.42x40.64mm (2300x1600mil) packing all the onboard features.
- **2x18P pinout layout**, standard pitch 2.54mm (100mil) breadboard friendly, with one side dedicated for peripheral (power, programming, communication) and the other side for GPIO, simplifying wire/trace management.
- **Castellated holes & pin header**, choose inter-board connection method according to your application requirement.
- **ESP32-WROOM-32UE**, comes with latest [ECO V3](https://www.espressif.com/sites/default/files/documentation/ESP32_ECO_V3_User_Guide__EN.pdfhttps://www.espressif.com/sites/default/files/documentation/ESP32_ECO_V3_User_Guide__EN.pdf) Dual Core 32-bit LX6 microprocessor with clock up to 240MHz, ULP co-processor, 520kB SRAM, 4MB flash.
- **802.11b/g/n WiFi Connectivity**, support mode STA/AP/STA+AP mode with external antenna using U.FL/IPEX connector allowing the board to be installed inside the enclosure without worrying transceiver signal quality. 
- **Bluetooth 4.2 Connectivity**, support classic bluetooth and Low Energy (LE) protocol.
- **CP2104 UART to USB Bridge**, full-speed programmer & data port with auto-reset trigger using DTR and RTS line.
- **DS3231M RTC**, extremely accurate ±5ppm RTC with alarm trigger capability and replaceable CR1220 battery. Connected via I2C at address 0x68.
- **AHT20 Environment Sensor**, temperature and humidity sensor connected via I2C at address 0x38.
- **XC6220 LDO**, providing +3.3V power up to 1A with Green Operation mode which automatically switched to power save mode on light load.
- **Built-in LED/RGB**, single color active-low LED connected to pin IO2, and SK6812 addressable RGB LED connected to pin IO4. SK6812 data out is exposed so you can chain it up with the rest of the LED circuit.
- **MicroSD socket**, connected via SPI with slave select (SS) at pin IO5.
- **USB Type-C Connector**, no more hassle when connecting USB cable, plug it in anyway you want.
- **26 pin GPIO** @3V3 level, 3xUART, 2xSPI, 2xI2C, 2xI2S, 12bit ADC, 8bit DAC, hall-effect sensing, capacitive sensing, JTAG debug, etc. Please see pinout poster/schematic file for more information.

## How to Use
### Installing USB-UART Driver
Normally the CP2104 driver is automatically recognized and/or installed by Windows Update (for Windows OS). But if you have a problem, you can install it manually by downloading the latest driver here https://www.silabs.com/developers/usb-to-uart-bridge-vcp-drivers. The step is straight forward, download the file and click the executable file to install the driver.  

After this, you should see the serial communication device (and port number) both on your system (device manager) or in the Arduino IDE software. You can skip this step if you already install the driver.

### Installing ESP32 Hardware Package
Chip from Espressif doesn't supported out-of-the-box by Arduino IDE so we need 3rd-party hardware package called ESP32 Arduino Core. The package installed using board manager, for detailed instruction on how to install ESP32 Arduino Core on Arduino IDE you can follow the step here
https://github.com/espressif/arduino-esp32/blob/master/docs/arduino-ide/boards_manager.md.

Once it's done, ESP32 should be listed on the board selection menu. Choose **ESP32 Dev Module** on board option, **4MB (32Mb)** on the flash size option and set the PSRAM option to disabled. For the partition scheme (application memory & file system) you can choose the allocation combination as needed, and the other option can left as default.  
<img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-arduinoideinfo.png" width="600">  
Now your SENTSOR Core ESP32-DEV is ready to be use! Again, you can skip this step if you already install the ESP32 hardware package.

### Dependency
To access on-board peripheral like RTC, MicroSD, RGB LED & AHT20 sensor you may need to install related library below:
- RTCLib https://github.com/adafruit/RTClib
- SdFat https://github.com/greiman/SdFat
- NeoPixel https://github.com/adafruit/Adafruit_NeoPixel
- AHT20 https://github.com/adafruit/Adafruit_AHTX0

or any other library of your choice that have same functionality.

## Bill of Materials
|Designator|Qty|Name/Value|Footprint|
|-|-|-|-|
|U1|1|CP2104-F03-GMR|QFN-24_L4.0-W4.0-P0.50-EP2.6|
|U2|1|XC6220B331MR-G|SOT-25-5_L3.0-W1.8-P0.95|
|U3|1|ESP32-WROOM-32UE(4MB)|WIFIM-32UE-SMD_38P|
|U4|1|DS3231MZ+|SOIC-8_L4.9-W3.9-P1.27|
|U5|1|AHT20|DFN-6_L3.0-W3.0-P1.00|
|R1|1|1M|R0402|
|R2,R3|2|5.1k|R0402|
|R4,R5,R8,R17|4|1k|R0402|
|R6,R9,R10,R11,R12, R13,R14,R15,R16|9|10k|R0402|
|R7|1|100k|R0402|
|C1,C8,C10,C11,C12,C13,C14|7|100n|C0402|
|C2,C6|2|4.7u|C0402|
|C3,C4,C5,C9|4|10u|C0402|
|C7|1|220u, 6.3V|CASE-B_3528|
|D1|1|B5819WS|SOD-323_L1.8-W1.3|
|D2|1|USBLC6-2SC6|SOT-23-6_L2.9-W1.6-P0.95|
|LED1,LED2|2|Blue|LED0402|
|LED3,LED4|2|White|LED0402|
|LED5|1|EC20-SK6812|LED2020|
|Q1|1|UMH3N|SC-70-6_L2.2-W1.3-P0.65|
|BTN1,BTN2|2|3.9x3x4.45|SW-SMD_L3.9-W3.0-P4.45|
|CN1|1|TYPEC-304S-ACP16|USB-C-SMD|
|CARD1|1|HYC80-TF08-375|HYC80-TF08-XXX|
|BAT1|1|CR1220|BAT_CR1220_SMD|

## Design 
<img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-pcb-ss.png" width="600">  

SENTSOR Core ESP32-DEV is an open source hardware, please use it wisely. The project files is hosted on online based EDA called EasyEDA, you can access it via link below:  

Link: https://easyeda.com/sentsor-project/sentsor-core-esp32-dev

## Gallery
_Render View:_  
<img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-render0.png" width="400"> <img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-render1.png" width="400">  
<img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-render2.png" width="400"> <img src="https://github.com/adamalfath/sentsor-core-esp32dev/blob/main/media/esp32dev-render3.png" width="400">

## Support Open Source Hardware & SENTSOR!
If you are interested in our product, you can buy them in the marketplace or by giving donation using this link below:

[![Store](https://img.shields.io/badge/marketplace-Tokopedia-brightgreen.svg)](https://www.tokopedia.com/gerai-sagalarupa/etalase/sentsor-product)  [![Store](https://img.shields.io/badge/marketplace-Tindie-lightgrey.svg)](https://www.tindie.com/)  [![Donate](https://img.shields.io/badge/donate-PayPal-blue.svg)](https://www.paypal.me/adamalfath)  

Your support will be very helpful for the next development of open source hardware from SENTSOR.

## Information
SENTSOR  
Author: Adam Alfath  
Contact: adam.alfath23@gmail.com  
Web: [sentsor.net](http://www.sentsor.net)  
Repo: [SENTSOR Main Repo](http://github.com/adamalfath/sentsor)

<img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/80x15.png"/></a><br/>
SENTSOR Core ESP32-DEV is licensed under <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.
