# Tuya-TH04-PHY6252-1.5-teardown
![Image](https://github.com/user-attachments/assets/ba480c1a-26d1-43f0-b91d-9b4272e6b7a7)

Beautiful, minimalistic and clean PCB layout. 

Issue estabilishing reliable readouts in tuya app, seems it is broken when leaving app first time.
Someone wrote on similar product info that "registration with email in china mainland" was required for it to work, not tried.

GTRV test points map to:
G = GND
T = TX
R = RX
V = Vcc Voltage input

Tested connection using USB to 3.3V UART. Using 1000000 baud and script du dump firmware:
[https://github.com/pvvx/PHY62x2/tree/master/Utils](https://github.com/pvvx/PHY62x2/tree/master/Utils)


Main chip: PHY6252
Sensor: AHT20
LCD Driver: Vinka VKL060

More information related to PHY6252:
[https://github.com/duanmubingshuai/test](https://github.com/duanmubingshuai/test)

[https://github.com/sullivan986/phy6252-SDK](https://github.com/sullivan986/phy6252-SDK)

[https://github.com/pvvx/PHY62x2](https://github.com/pvvx/PHY62x2)



More information related to AHT20:
The AHT20 is a high-precision, low-cost temperature and humidity sensor communicating using I2C bus
[AHT20-datasheet-2020-4-16.pdf](https://cdn-learn.adafruit.com/assets/assets/000/091/676/original/AHT20-datasheet-2020-4-16.pdf?1591047915)

More information related to Vinka VKL060:
The VKL060 is a RAM Mapping LCD Driver capable of supporting LCD screens with a maximum of 60 patterns (15SEG x 4COM)
[https://szvinka.com/uploadfile/Datasheet/LCD/VKL060/VKL060_V1.3-EN.pdf](https://szvinka.com/uploadfile/Datasheet/LCD/VKL060/VKL060_V1.3-EN.pdf)
