# The Server-With-a-PiKVM Project 

- [1.0 Introduction](https://github.com/etkaar/pikvm)
- [2.0 Pictures](https://github.com/etkaar/pikvm)

## 3.0 Requirements

### 3.1 The Basic Hardware

- **Server Case** with 2U or more. This project uses the UNYKAch 2128.

  🏬 Suppliers: [Amazon.de](https://www.amazon.de/UNYKAch-2128-19-2U-Geh%C3%A4use-Computer-Geh%C3%A4use-Geh%C3%A4use-Micro-ATX/dp/B079XY9SMQ)

- **Mainboard**: To leave enough space, you might choose one with form factor microATX (mATX).

- **Raspberry Pi 4**

  - In order to control both the keyboard and the mouse of the server, we will need a Raspberry Pi which offers USB On-The-Go (OTG). This way, the Raspberry will act as an external USB device and will simulate a keyboard, mouse (and mass storage for images):
  
    <img src="https://user-images.githubusercontent.com/40885610/221382600-c39dca19-fec1-4946-8ad5-dfd50eaa02fd.png" width="500">
    
    The default name is "PiKVM CD-ROM Drive 0515".
  
    **USB On-The-Go (OTG)**
    
    Following Raspberry Pis offer OTG:

     - [Raspberry Pi 4 Model B](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) via USB-C: The one we will use. It is recommended to use the 2 GB version.
    
     - [Raspberry Pi Zero 2 W](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/) via Micro-USB: No Ethernet port.
     - [Raspberry Pi Zero W](https://www.raspberrypi.com/products/raspberry-pi-zero-w/) via Micro-USB: No Ethernet port and is legacy.
     - [Raspberry Pi Zero](https://www.raspberrypi.com/products/raspberry-pi-zero/) via Micro-USB: No Ethernet port and not supported by PiKVM.

    
    Following do **not** offer OTG and therefore are not recommended:
    
     - Raspberry Pi Pico
     - Raspberry Pi Pico W
     - Raspberry Pi 1 Model A
     - Raspberry Pi 1 Model A+
     - Raspberry Pi 1 Model B
     - Raspberry Pi 1 Model B+
     - Raspberry Pi 2 Model B
     - Raspberry Pi 2 Model B V1.2
     - Raspberry Pi 3 Model A+
     - Raspberry Pi 3 Model B
     - Raspberry Pi 3 Model B+

- **3D Printer**

  Reliable and cheap is a FLSUN Q5.

  - **PCTG Filament**: You will also need a special filament. While PLA is a great filament, this is not what we want in our case. Instead, we will use a special PCTG filament which not only is more temperature stable (about 80-90 °C), but also offers flame-retardant properties according to [UL94 V2](https://en.wikipedia.org/wiki/UL_94). Still, it is very unlikely that anything will ever happen – but having anything easily inflammable in a server is never good practice.

    - Extrudr PCTG, 1.75 mm, 0.8 kg<br>
      🏬 Suppliers: [extrudr.com](https://www.extrudr.com/en/products/catalogue/pctg-blau_3642/) (Official Store), [Amazon.de](https://www.amazon.de/s?k=Extrudr+PCTG&__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&ref=nb_sb_noss)<br>

  - **Polyimide Tape**: While you don't need a 3D printer with a closed chamber, it can be hard to print PCTG to the surface as it tends to not stick or only stick at very high build temperatures. Therefore, you will need Polyimide tape (also known as "Kapton"). This allowed me to lower the build plate temperature to only 70 °C while using 250 °C for the nozzle. The tape can be used for multiple prints: It is neither required to remove it after printing, nor is it required to clean it with isopropyl alcohol afterwards.
  
    <img src="https://user-images.githubusercontent.com/40885610/221425578-d31c160f-f979-4edc-963e-295ae1455ff0.JPG" width="400">
  
### 3.2 Tools

- **Soldering Iron** or a **Soldering Station**

  An ERSA i-CON nano does a great job. It is small and ESD protected. I primarily use it with the tips [0102PDLF10](https://www.ersa-shop.com/ersa-ersadur-l%C3%B6tspitze-f%C3%BCr-itool-gerade-bleistiftspitz-p-1316.html) (pointed, 1.0 mm), [0102ADLF13](https://www.ersa-shop.com/ersa-ersadur-l%C3%B6tspitze-f%C3%BCr-itool-gerade-angeschr%C3%A4gt-p-1723.html) (beveled, 1.3 mm) and [0102CDLF16](https://www.ersa-shop.com/ersa-ersadur-l%C3%B6tspitze-f%C3%BCr-itool-gerade-mei%C3%9Felf%C3%B6rmig-p-819.html) (chisel-shaped, 1.6 mm).
  
- **Soldering Tin**

  I can recommend *armack Typ32-3* (S-Sn95Ag4Cu1) with 0.5 and 0.8 mm. Contains silver, but not lead. I set the soldering station to 315 °C.
  
  🏬 Suppliers: [display3000.com](https://display3000.com/shop/werkstatt/loetzinn-lote/bleifreies-loetzinn-2-4.html)

- **Automatic Wire Stripper**: For instance, the one from WEICON tools.

  🏬 Suppliers: [Amazon.de](https://www.amazon.de/gp/product/B001NUMVHQ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)

### 3.3 Parts for the Raspberry Pi 4

- **HDMI to CSI-2 Module**

  This module is connected to the camera slot of the Raspberry using a FFC cable (Flat Flexible Cable) and to the server's HDMI port.
  
  - Search for: "Geekworm Raspberry Pi HDMI IN Module C779, HDMI to CSI CSI-2"<br>
     🏬 Suppliers: [Amazon.de](https://www.amazon.de/gp/product/B0899L6ZXZ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)<br>
  
- The **original power supply** (the one with the round cable) or any other stabilized power supply with a round cable providing 5 to 5.1 VDC, thick wires (18 AWG) and 2.5 to 3 A. Thicker wires are recommended because of the voltage drop which can occur at long distances and high current draw. The round cable is required for the assembly of the neutriCON connector. Since we don't use the USB-A ports, 2.5 A is reasonable, even for a hungry Raspberry Pi 4.

- **microSD Card** with 64 GB.

### 3.3.1 Part for the Frontpanel Header Control

1. **Prototyping HAT / Raspberry Pi Shield**

   This is a breadboard put onto the Raspberry. It makes it easy for you to solder the frontpanel header control schematic (required to start or restart the server) and connect it to the according GPIO pins.
  
    - Search for: "GeeekPi 4x Prototype Breakout DIY Breadboard PCB Shield Board Kit"<br>
       🏬 Suppliers: [Amazon.de](https://www.amazon.de/gp/product/B08C4XLT44/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1)<br>
     
       There *might* be better PCBs than the current version by GeekPi (February 2023). While it fits, soldering is easy and all required GPIOs are available, the recess for the FFC cable of the HDMI to CSI-2 module is not at the right position for a Raspberry Pi 4. However, this should not be a big problem because the FFC cable is usually long enough.

2. 4 x Omron G3VM-61A1 MOSFET Relay ([Datasheet](https://omronfs.omron.com/en_US/ecb/products/pdf/en-g3vm_61a1_d1.pdf))<br>
   🏬 Suppliers: [Reichelt.de](https://www.reichelt.de/mosfet-relais-spst-no-60-v-0-5-a-1-r-dip-4-g3vm-61a1-p314678.html)
3. 4 x Axial miniature resistor with 330 or 390 Ω, axial, size 0204 (about 3.5 mm = 0,13 inch).<br>
   🏬 Suppliers: [Reichelt.de](https://www.reichelt.de/de/de/duennschichtwiderstand-axial-0-4-w-330-ohm-1--vi-mba02040c3300-p233643.html)
5. 2 x Axial miniature 4.7K Ω, axial, size 0204 (about 3.5 mm = 0,13 inch)<br>
   🏬 Suppliers: [Reichelt.de](https://www.reichelt.de/de/en/metal-film-resistor-4-7-kohm-0204-0-4-w-1--yag-4fte52-4k7-p236963.html)
   
   Of course, you could also use SMD or MELF resistors if you can handle them.
   
   **Miniature *vs* Standard Size**
   
   <img src="https://user-images.githubusercontent.com/40885610/221437278-55a083f2-4c19-40f3-97fa-51b00bf41101.jpg" height="150">


      
