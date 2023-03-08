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
  
## 4.0 Assembly ▲ [Index](#index)

### 4.1 Control Board for the System Panel Header

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

### 4.1.1 Polarity

The polarity is only relevant for the Power and IDE/HDD LEDs. The power and reset buttons instead are just shorted to ground.

### 4.1.2 How the Control Board Works

