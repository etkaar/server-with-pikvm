# The Server-With-a-PiKVM Project 

## Index

- [1.0 Introduction](https://github.com/etkaar/server-with-pikvm)
- [2.0 Pictures](https://github.com/etkaar/server-with-pikvm)
- 3.0 Requirements
  - [3.1 The Basic Hardware](https://github.com/etkaar/server-with-pikvm/blob/main/Requirements.md#31-the-basic-hardware)
  - [3.2 Tools](https://github.com/etkaar/server-with-pikvm/blob/main/Requirements.md#32-tools)
  - [3.3 Parts for the Raspberry Pi 4](https://github.com/etkaar/server-with-pikvm/blob/main/Requirements.md#33-parts-for-the-raspberry-pi-4)
    - [3.3.1 Parts for the System Panel Header Control Board](https://github.com/etkaar/server-with-pikvm/blob/main/Requirements.md#331-parts-for-the-system-panel-header-control-board)
  - [3.4 Cables, Connectors, Terminals, i.e.](https://github.com/etkaar/server-with-pikvm/blob/main/Requirements.md#34-cables-connectors-terminals-ie)
- 4.0 Assembly
  - [4.1 Control Board for the System Panel Header](https://github.com/etkaar/server-with-pikvm/blob/main/Assembly.md#41-control-board-for-the-system-panel-header)

## 3.0 Requirements ▲ [Index](#index)

### 3.1 The Basic Hardware

- **Server Case** with 2U or more. This project uses the [UNYKAch 2128](https://unykach.com/en/professional/rack19/rack-case-2u19-uk-2129-52095/).

  🏬 [Amazon.de](https://www.amazon.de/UNYKAch-2128-19-2U-Geh%C3%A4use-Computer-Geh%C3%A4use-Geh%C3%A4use-Micro-ATX/dp/B079XY9SMQ)

- **Mainboard**: To leave enough space, you might choose one with form factor microATX (mATX).

- **Raspberry Pi 4**

  - In order to control both the keyboard and the mouse of the server, we will need a Raspberry Pi which offers USB On-The-Go (OTG). This way, the Raspberry will act as an external USB device and will simulate a keyboard, mouse (and mass storage for images):
    
    Following Raspberry Pis offer OTG and are supported:

     - [Raspberry Pi 4 Model B](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) via USB-C: The one we will use. It is recommended to use the 2 GB version, though 1 GB should also work.
     - [Raspberry Pi Zero 2 W](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/) via Micro-USB: No Ethernet port.
    
    While they offer OTG, they are either considered as legacy or not supported:
    
    - [Raspberry Pi Zero W](https://www.raspberrypi.com/products/raspberry-pi-zero-w/) via Micro-USB: No Ethernet port and is considered as legacy since Arch Linux ARM [has dropped support](https://archlinuxarm.org/forum/viewtopic.php?f=3&t=15721) for ARMv5 and ARMv6 architectures in February 2022. The Zero without W is not supported at all by PiKVM.

- **3D Printer**

  Reliable and cheap is an FLSUN Q5.

  - **PCTG Filament**: You will also need a special filament. While PLA is a great filament, this is not what we want in our case. Instead, we will use a special PCTG filament which not only is more temperature stable (about 80-90 °C), but also offers flame-retardant properties according to [UL94 V2](https://en.wikipedia.org/wiki/UL_94). Still, it is very unlikely that anything will ever happen – but having anything easily inflammable in a server is never good practice.

    - Extrudr PCTG, 1.75 mm, 0.8 kg<br>
      🏬 [extrudr.com](https://www.extrudr.com/en/products/catalogue/pctg-blau_3642/) (Official Store), [Amazon.de](https://www.amazon.de/s?k=Extrudr+PCTG&__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&ref=nb_sb_noss)<br>

  - **Polyimide Tape**: While you don't need a 3D printer with a closed chamber, it can be hard to print PCTG to the surface as it tends to not stick or only stick at very high build temperatures. Therefore, you will need Polyimide tape (also known as "Kapton"). This allowed me to lower the build plate temperature to only 70 °C while using 250 °C for the nozzle. The tape can be used for multiple prints: It is neither required to remove it after printing, nor is it required to clean it with isopropyl alcohol afterwards.
  
    <img src="https://user-images.githubusercontent.com/40885610/221425578-d31c160f-f979-4edc-963e-295ae1455ff0.JPG" width="400">
  
---
  
### 3.2 Tools

- **Soldering Iron** or a **Soldering Station**

  An ERSA i-CON nano does a great job. It is small and ESD protected. I primarily use it with the tips [0102PDLF10](https://www.ersa-shop.com/ersa-ersadur-l%C3%B6tspitze-f%C3%BCr-itool-gerade-bleistiftspitz-p-1316.html) (pointed, 1.0 mm), [0102ADLF13](https://www.ersa-shop.com/ersa-ersadur-l%C3%B6tspitze-f%C3%BCr-itool-gerade-angeschr%C3%A4gt-p-1723.html) (beveled, 1.3 mm) and [0102CDLF16](https://www.ersa-shop.com/ersa-ersadur-l%C3%B6tspitze-f%C3%BCr-itool-gerade-mei%C3%9Felf%C3%B6rmig-p-819.html) (chisel-shaped, 1.6 mm).
  
- **Soldering Tin**

  I can recommend *armack Typ32-3* (S-Sn95Ag4Cu1) with 0.5 and 0.8 mm. Contains silver, but not lead. I set the soldering station to 315 °C.
  
  🏬 [display3000.com](https://display3000.com/shop/werkstatt/loetzinn-lote/bleifreies-loetzinn-2-4.html)

- **Automatic Wire Stripper**: For instance, the one from WEICON tools.

  🏬 [Amazon.de](https://www.amazon.de/gp/product/B001NUMVHQ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)

---

### 3.3 Parts for the Raspberry Pi 4

- **HDMI to CSI-2 Module**

  This module is connected to the camera slot of the Raspberry using a FFC cable (Flat Flexible Cable) and to the server's HDMI port.
  
  The Geekworm X630 V1.5 (Option A) was released in December 2022 and therefore seems to be the newest version in March 2023. It is also smaller and easier to install. See also the according Wiki Article:   https://wiki.geekworm.com/X630
  
  **Option A:** "Geekworm Raspberry Pi Hdmi to CSI-2 Module X630" (5 cm FFC cable)<br>
     🏬 [Amazon.de](https://www.amazon.de/dp/B09H2N99VL?psc=1&ref=ppx_yo2ov_dt_b_product_details)<br>
  
  **Option B:** "Geekworm Raspberry Pi HDMI IN Module C779, HDMI to CSI CSI-2" (15 cm FFC cable)<br>
     🏬 [Amazon.de](https://www.amazon.de/gp/product/B0899L6ZXZ/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1)<br>
  
- The **Original Power Supply** (the one with the round cable) or any other stabilized power supply with a round cable providing 5 to 5.1 VDC, thick wires (18 AWG) and 2.5 to 3 A. Thicker wires are recommended because of the voltage drop which can occur at long distances and high current draw. The round cable is required for the assembly of the neutriCON connector. Since we don't use the USB-A ports, 2.5 A is reasonable, even for a hungry Raspberry Pi 4.

- **microSD Card** with 64–128 GB.

---

### 3.3.1 Parts for the System Panel Header Control Board

1. **Prototyping HAT / Raspberry Pi Shield**

   This is a breadboard put onto the Raspberry. It makes it easy for you to solder the frontpanel header control schematic (required to start or restart the server) and connect it to the according GPIO pins.
  
    - Search for: "GeeekPi 4x Prototype Breakout DIY Breadboard PCB Shield Board Kit"<br>
       🏬 [Amazon.de](https://www.amazon.de/gp/product/B08C4XLT44/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1)<br>
     
       There *might* be better breadboards than the current version by GeekPi (February 2023). While it fits, soldering is easy and all required GPIOs are available, the recess for the FFC cable of the HDMI to CSI-2 module is not at the right position for a Raspberry Pi 4. However, this can be compensated by using a longer FFC cable (10 cm or more).
       
    <img src="https://user-images.githubusercontent.com/40885610/221559192-b8c10a05-55af-447d-8d77-3d311936cb9c.jpg" width="500">

2. 4 x Omron G3VM-61A1 MOSFET Relay ([Datasheet](https://omronfs.omron.com/en_US/ecb/products/pdf/en-g3vm_61a1_d1.pdf))<br>
   🏬 [Reichelt.de](https://www.reichelt.de/mosfet-relais-spst-no-60-v-0-5-a-1-r-dip-4-g3vm-61a1-p314678.html)
   
   <img src="https://user-images.githubusercontent.com/40885610/221562800-ad3a05e4-d9ce-446c-a558-63cf4fb78b76.jpg" width="500">
   
3. 4 x Axial miniature resistor with 330 or 390 Ω, axial, size 0204 (about 3.5 mm = 0.13 inch).<br>
   🏬 [Reichelt.de](https://www.reichelt.de/de/de/duennschichtwiderstand-axial-0-4-w-330-ohm-1--vi-mba02040c3300-p233643.html)
5. 2 x Axial miniature 4.7K Ω, axial, size 0204 (about 3.5 mm = 0.13 inch)<br>
   🏬 [Reichelt.de](https://www.reichelt.de/de/en/metal-film-resistor-4-7-kohm-0204-0-4-w-1--yag-4fte52-4k7-p236963.html)
   
   Of course, you could also use SMD or MELF resistors if you can handle them.
   
   **Miniature *vs* Standard Size**

   <img src="https://user-images.githubusercontent.com/40885610/221559339-6090bde7-7353-4aa0-b6d6-2d05dcee0837.jpg" height="150">

---

### 3.4 Cables, Connectors, Terminals, i.e.
      
- **HDMI Cable**, 1.0 meter

- **FFC Cable**, 10 cm long if you use the X630 HDMI to CSI-2 module, as the included cable is only 5 cm long.
      
- **Stranded Tinned Copper Wires**

  23 AGW (0.25 mm²) in five colors: Blue + Yellow + White + Red + Black

- **Solid (Tinned) Copper Wires**

  19–21 AWG (0.5 mm²) in four colors: Blue + Red + Yellow + White
  
- **USB-C to USB-A 2.0 cable**, 0.5–1.0 meter

  This cable will later be modified and used for OTG.
  
### 3.5 Parts for the Server Case  
  
- **Ethernet Patch Cable**, 0.5–1.0 meter
  
- **Power Connectors for Raspberry Pi Power Supply <-> Server Case**

  The male chassis connector is connected to the server case, while the female cable connector is connected to the cable of the power supply for the Raspberry Pi.

  **neutriCON**

  | Name | Product Code | Max. Current<sup>1</sup> | Max. Wire Size |
  | :-- | :-- | :--: | :--: |
  | neutriCON 8-pole Male Chassis Connector | [ORP8M-NI](https://www.neutrik.com/en/product/orp8m-ni) (Nickel) *or* [ORP8M](https://www.neutrik.com/en/product/orp8m) (Black) | 7.5 A | 18 AWG (1.0 mm²) |
  | neutriCON 8-pole Female Cable Connector | [OSC8F-NI](https://www.neutrik.com/en/product/osc8f-ni) (Nickel) *or* [OSC8F](https://www.neutrik.com/en/product/osc8f) (Black) | 7.5 A | 18 AWG (1.0 mm²) |
  
  *OR*
  
  **XLR-4**
  
    | Name | Product Code | Max. Current<sup>1</sup> | Max. Wire Size |
  | :-- | :-- | :--: | :--: |
  | Neutrik 4-pole Male Chassis Connector | [NC4MD-LX](https://www.neutrik.com/en/product/nc4md-lx) (Nickel) *or* [NC4MD-LX-B](https://www.neutrik.com/en/product/nc4md-lx-b?c=audio) (Black) | 10 A | 16 AWG (1.5 mm²) |
  | Neutrik 4-pole Female Cable Connector | [NC4FXX](https://www.neutrik.com/en/product/nc4fxx) (Nickel) *or* [NC4FXX-B](https://www.neutrik.com/en/product/nc4fxx-b) (Black) | 10 A | 16 AWG (1.5 mm²) |
  
  <sup>1</sup> Rated current per contact.
  
- **RJ45 Pass-through Chassis Connector**

    | Name | Product Code | Category |
  | :-- | :-- | :--: |
  | etherCON RJ45 Chassis Connector | [NE8FDP](https://www.neutrik.com/en/product/ne8fdp) (Nickel) *or* [NE8FDP-B](https://www.neutrik.com/en/product/ne8fdp-b) (Black) | Cat 5e |
  


