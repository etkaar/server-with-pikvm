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
