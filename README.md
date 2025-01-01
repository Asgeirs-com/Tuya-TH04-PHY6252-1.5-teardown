# Tuya-TH04-PHY6252-1.5-teardown
![Image](https://github.com/user-attachments/assets/ba480c1a-26d1-43f0-b91d-9b4272e6b7a7)

Beautiful, minimalistic and clean PCB layout.   
Main chip: PHY6252    
Sensor: AHT20    
LCD Driver: Vinka VKL060  



Issue estabilishing reliable bluetooth readouts in tuya app, seems it is broken when leaving app first time.
Someone wrote on similar product info that "registration with email in china mainland" was required for it to work, not tried.



G,T,R,V test points map to:

G = GND  
T = TX  
R = RX    
V = Vcc Voltage input  


Tested connection using USB to 3.3V UART. Using 1000000 baud and script du dump firmware:  
[https://github.com/pvvx/PHY62x2/tree/master/Utils](https://github.com/pvvx/PHY62x2/tree/master/Utils)

No reset test point, so had to cut power. First attempt to cut power using Vcc failed, because enough power was sourced trough the serial RX/TX lines:  

C:\PHY62x2-master\Utils>python rdreg_phy6252.py -p COM3 -b 1000000 0x11000000 0x80000  
RdRegs-PHY62x2 Utility version 23.11.22  
PHY62x2 - Error Reset!    
Check connection TX->RX, RX<-TX and Chip Power!


When cutting ground connection, reset was successfull, but dump failed first try: 

C:\PHY62x2-master\Utils>python rdreg_phy6252.py -p COM3 -b 1000000 0x11000000 0x80000  
RdRegs-PHY62x2 Utility version 23.11.22  
PHY62x2 - Reset Ok  
PHY62x2 - Error init1!  


Success in doing somthing second attampt:  

C:\PHY62x2-master\Utils>python rdreg_phy6252.py -p COM3 -b 1000000 0x11000000 0x80000  
RdRegs-PHY62x2 Utility version 23.11.22  
PHY62x2 - Reset Ok  
Reopen COM3 port 1000000 baud  
Revision: b'0x001340c4'  
Start address: 0x11000000, length: 0x00080000  
  Time: 1065.948 sec    
Writes: 1704206 Bytes  
 Reads: 2228248 Bytes    
512.000 KBytes saved to file 'r11000000-00080000.bin'  



But bin file contains strange info, so probably something failed:  
snip/  
  [Hard fault handler]  
  R0-R3        = 0x%08x 0x%08x 0x%08x 0x%08x  
 R4-R7        = 0x%08x 0x%08x 0x%08x 0x%08x  
 R8-R11       = 0x%08x 0x%08x 0x%08x 0x%08x  
 R12,SP,LR,PC = 0x%08x 0x%08x 0x%08x 0x%08x  
 PSR  = 0x%08x    í àICSR = 0x%08x  
  ´ÿ`ÿ[OSAL]idx %d Func 0x%08x systick %08x rtc %08x  
     -----------dump stack--------------  
/snip  
[zipped copy of r11000000-00080000.bin](https://github.com/Asgeirs-com/Tuya-TH04-PHY6252-1.5-teardown/edit/main/r11000000-00080000.zip)  


Chip info:  
C:\PHY62x2-master\Utils>python rdwr_phy62x2.py -p COM3 -b 1000000 i  
=========================================================  
PHY62x2 Utility version 09.01.24  
---------------------------------------------------------  
Connecting...  
PHY62x2 - Reset Ok  
Revision: b'001340c4 6222M005'  
FlashID: 1340c4, size: 512 kbytes  
PHY62x2 - connected Ok  
Reopen COM3 port 1000000 baud... ok  




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
