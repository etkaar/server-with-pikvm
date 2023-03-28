## 5.0 Stresstests

Stressing a Raspberry Pi 4 is easy, even if a PiKVM based on Arch Linux ARM is used. You can install `stressberry` by using following command:

```
rw
pacman -S stressberry
ro
```

The `rw` (read & write) and `ro` (read-only) commands are only used to disable and enable the ready-only mode of the file system.

⚠️ **Do not forget to enable read-only mode again once your work is finished.**

Use following command to run a one-hour stress test preceded and followed by a five-minute idle period:

```
stressberry-run -n "PiKVM" -d 3600 -i 300 -c 4 pikvm.out
```

With following command you can create a PNG image of the result:

```
stressberry-plot pikvm.out -f -d 300 -f -l 400 1600 -t 30 90 -o pikvm.png
```

---

### 5.1 Server Turned Off (No Fans)

As expected, the Raspberry Pi 4 gets quite hot, with the CPU hitting almost 176 °F (80 °C):

---

### 5.2 Running Server

With a running server and spinning fans then that's a completely different story.

---

### 5.3 Summary

In both cases, no throttling takes place at a room temperature of about 68 °F (20 °C). All four cores are running at 1,5 GHz:

![top](https://user-images.githubusercontent.com/40885610/228374420-c8e648c4-40a2-474a-823a-8b894a03ccfd.png)
![CPUFrequ](https://user-images.githubusercontent.com/40885610/228374433-6b904005-a047-4491-acd5-01caa752cf6a.png)
