## 4.2 GPIO Header Power Cable (4-pin, 50 cm)

Regardless of how we power the RPi 4 we need a power cable which is attached to our power connector we assambled onto the server case (e.g. neutriCON or XLR-4). We use two 23 AGW (0.25 mm²) wires each for red (VCC) and black (ground). There are two reasons for that: On one hand, we simply want to prevent any voltage drop. But on the other hand, having the cable plugged to only *two* pins on the GPIO header doesn't really look stable. Using four pins is safer.

![PowerCable](https://user-images.githubusercontent.com/40885610/228363726-0ea5f723-b60f-4103-9e91-ee1d5fe504ad.jpg)


  | State | Voltage |
  | :-- | :-- |
  | Idle | 5.22 V |
  | Stress | 5.11 V |
