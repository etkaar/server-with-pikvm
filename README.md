# The Server-With-a-PIKVM Project 

In this article I will explain how you can build a server with a KVM using a Raspberry Pi 4 and PiKVM OS. [PiKVM](https://pikvm.org/) is a great open-source project people - including me - have been waiting years for.

## 1.0 Introduction

As the goal of this project is to make it as professional and replicable as possible, you will definitely need:

- Interest and motivation
- A great amount of time
- Not too less money

This article does neither contain paid advertisement, nor referral links (e.g. to Amazon or other sites).

## 2.0 Requirements

- Raspberry Pi 4

  - In order to control both the keyboard and the mouse of the server, we will need a Raspberry Pi which offers USB On-The-Go (OTG). This way, the Raspberry will act as an external USB device and will simulate a keyboard, mouse (and mass storage for images):
  
    <img src="https://user-images.githubusercontent.com/40885610/221382600-c39dca19-fec1-4946-8ad5-dfd50eaa02fd.png" width="500">
    
    The default name is "PiKVM CD-ROM Drive 0515".
  
    Following Raspberry Pis offer OTG:
    
     - [Raspberry Pi Zero](https://www.raspberrypi.com/products/raspberry-pi-zero/) via Micro-USB
     - [Raspberry Pi Zero W](https://www.raspberrypi.com/products/raspberry-pi-zero-w/) via Micro-USB
     - [Raspberry Pi Zero 2 W](https://www.raspberrypi.com/products/raspberry-pi-zero-2-w/) via Micro-USB
     - [Raspberry Pi 4 Model B](https://www.raspberrypi.com/products/raspberry-pi-4-model-b/) via USB-C
    
    Following do **not** offer it and therefore are not recommended:
    
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

- 3D printer: Reliable and cheap is a FLSUN Q5.

  - **PCTG Filament**: You will also need a special filament. While PLA is a great filament, this is not what we want in our case. Instead, we will use a special PCTG filament which not only is more temperature stable (about 80-90 °C), but also offers flame-retardant properties according to [UL94 V2](https://en.wikipedia.org/wiki/UL_94). Still, it is very unlikely that anything will ever happen – but having anything easily inflammable in a server is never good practice.

    - Extrudr PCTG, 1.75 mm, 0.8 kg<br>
      🏬 Suppliers: [extrudr.com](https://www.extrudr.com/en/products/catalogue/pctg-blau_3642/) (Official Store), [Amazon.de](https://www.amazon.de/s?k=Extrudr+PCTG&__mk_de_DE=%C3%85M%C3%85%C5%BD%C3%95%C3%91&ref=nb_sb_noss)<br>

  - **Polyimide Tape**: While you don't need a 3D printer with a closed chamber, it can be hard to print PCTG to the surface. Therefore, you will need Polyimide tape (also known as "Kapton").
  
      
      
