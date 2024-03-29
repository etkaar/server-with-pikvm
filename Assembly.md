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
  - [4.2 USB 2.0 OTG Cable](https://github.com/etkaar/server-with-pikvm/blob/main/Assembly.md#42-usb-20-otg-cable)
  
## 4.0 Assembly ▲ [Index](#index)

### 4.1 Control Board for the System Panel Header

### 4.1.1 Introduction

This board is required to allow PiKVM to control the system panel header (sometimes also referred to as "front panel header") of the server:

<img src="https://user-images.githubusercontent.com/40885610/223600895-e75e943e-1cfe-4b8e-8ee5-86cccdbd3e07.png" width="500">

The front panel header (5 x 2) was standardized by Intel and consists of 9 pins where usually only 8 are in use:

  |  | Pin |  |  |
  | :-- | :-- | :-- | :-- |
  |  |  | 9 | NC (Not connected) *or* used as CI (-) |
  | Ground (GND) (Power) | 8 | 7 | Reset Button (HWRST#) (+) |
  | Power Button (PWR_BTN) (+) | 6 | 5 | Ground (GND) (Reset) |
  | Power LED (-) | 4 | 3 | IDE/HDD LED (-) |
  | Power LED (+) | 2 | 1 | IDE/HDD LED (+) |

While most of the mainboard manufacturers (ASUS, Gigabyte, MSI) follow this standard, some older mainboards from Biostar (before 2020) and Supermicro mainboards do not. Thus, you should double-check with your mainboards manual.

### 4.1.2 Polarity

The polarity is only relevant for the Power and IDE/HDD LEDs. The power and reset buttons instead are just shorted to ground.

### 4.1.3 Colors and GPIOs

In order to make it a little bit more obvious, we will use differentr colors for each role of the system panel header. The GPIO pins we use are the default pins defined in *get_plugin_options()* of [kvmd/plugins/atx/gpio.py](https://github.com/pikvm/kvmd/blob/master/kvmd/plugins/atx/gpio.py).

  | Color | Use Case | GPIO |
  | :-- | :-- | :--: |
  | Blue | Power Button | 23 |
  | Red | Reset Button | 27 |
  | Yellow | Power LED | 24 |
  | White | IDE/HDD LED | 22 |
  
### 4.1.4 Layout/Soldering

Solder all the components together as shown in the photo below.

1. Note, that the first two OMRON MOSFET Relays for the Power Button (Blue) and Reset Button (Red) are placed in **opposite** direction.
2. You only need to assemble the parts for the Power LED (Yellow) and IDE/HDD LED (White) if you want to have their values (glowing of the Power LED, blinking of the IDE/HDD LED) to be reflected in the PiKVM Web Interface.
3. The diode is optional, see below.
  
<img src="https://user-images.githubusercontent.com/40885610/225312911-7ad6c10d-3f13-4f2f-a919-8b22704e4267.jpg" width="800">

### Schottky Diode

The large diode is a Schottky diode (20 V, 5 A). It is placed anti-parallel and serves as a simple protection against reverse polarity. In this case, the diode causes a (deliberate) short circuit, which then causes the power supply to switch to the overload or short-circuit state. Therefore, you **must not** use power supplies which deliver more than the diode is able to withstand continuously. The Original Raspberry Pi power supplies with 3 A are suitable.

However, do not test it, even if the reverse voltage will be very low (between –0,3 and –0,1 V in my tests). It could be still harmful to sensitive components.

### 4.1.5 Cable (23 cm)

![FrontPanelCable](https://user-images.githubusercontent.com/40885610/224348197-e0fb5592-39d1-4da2-af23-1b9ac80f0042.jpg)

---  
  
## 4.2 USB 2.0 OTG Cable (32 cm)

We do not power the Raspberry Pi using its USB-C port, but we still make use of this port as this port offers OTG (USB On-The-Go) which is required for PiKVM to control the keyboard and mouse of the server and offer a mass storage device. Therefore, we still need to create our own cable from an USB-C <-> USB 2.0 cable with four (4) wires. Cables with only two wires are not suitable, as they only serve as power and not as data cable.

  | Color | Use Case |
  | :-- | :-- |
  | Red | VBUS (VCC) +5 V |
  | White | D- (Data) |
  | Green | D+ (Data) | 
  | Black | Ground (GND) |

⚠️ **It mandatory to disconnect the +5 V (VBUS/VCC) wire of the cable.**

You have two options:

A. Connecting the Raspberry from USB-C to a USB-A port of the server.<br>
B. Connecting the Raspberry from USB-C directly to the mainboard using an available USB 2.0 header.

### 4.2.1 Option A: USB-C to a USB-A

Remove a small portion of the cable's insulation and expose the individual wires. After that, cut the red cable for +5 V and also remove a small portion of it. For people like me with dyschromatopsia red and green is almost the same color:

![USBCToUSB2_P1](https://user-images.githubusercontent.com/40885610/223606007-359c4cc9-8a30-44a0-b445-0acff82d3eb2.jpg)

The next step is to protect the ends in order to prevent them from touching the shield of the cable which is connected to ground:

![USBCToUSB2_P2](https://user-images.githubusercontent.com/40885610/223606439-f3ace1fc-151b-4888-8f14-7cd5b6c82a4e.jpg)

At the end use polyimide (Kapton) tape to protect it. Don't use insulation tape – the adhesive is really awful and has caused my deaths due to this awfulness.

While the best method would be to use a heat shrink tube, that would usually require to cut *all* wires because even the USB-C plug will be the too large for the most heat shrink tubes appropriate to the small diameter of the cable. If you still don't like it, think about *option B*. 

![USBCToUSB2_P3](https://user-images.githubusercontent.com/40885610/223607259-f949a1b6-fbc3-47ee-a51c-8350911878c0.jpg)

![PiKVMCableUSB-A](https://user-images.githubusercontent.com/40885610/224345469-c3309ceb-d310-46a4-9482-898ad197f457.jpg)


### 4.2.2 Option B: USB-C to USB 2.0 header

This option makes the most sense for servers, because you won't be required to lead the cable outside of the case. You then can simply connect the Raspberry directly to the mainboards USB 2.0 header.

![PiKVMCableUSB-2 0Mainboard](https://user-images.githubusercontent.com/40885610/224345908-e5698d6d-0152-4256-aee4-5ca43468aa7e.jpg)

## 4.2 GPIO Header Power Cable (4-pin, 50 cm)

Regardless of how we power the RPi 4 we need a power cable which is attached to our power connector we assambled onto the server case (e.g. neutriCON or XLR-4). We use two 23 AGW (0.25 mm²) wires each for red (VCC) and black (ground). There are two reasons for that: On one hand, we simply want to prevent any voltage drop. But on the other hand, having the cable plugged to only *two* pins on the GPIO header doesn't really look stable. Using four pins is safer.

![PowerCable](https://user-images.githubusercontent.com/40885610/228363726-0ea5f723-b60f-4103-9e91-ee1d5fe504ad.jpg)


  | State | Voltage |
  | :-- | :-- |
  | Idle | 5.22 V |
  | Stress | 5.11 V |
