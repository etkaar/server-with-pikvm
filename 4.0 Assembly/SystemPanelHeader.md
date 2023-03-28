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
