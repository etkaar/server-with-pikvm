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
  - 
## 4.0 OS Imaging

PiKVM is not a software you will install on Raspberry Pi OS (formerly *Raspbian*). It is rather a lightweight OS, based on Arch Linux ARM.

For the Raspberry Pi 4 and Zero (2) W pre-compiled images [are available](https://pikvm.org/download). However, we will build the operating system ourselves. For that, you will need a x86-64 machine (or a virtual server). In this example Debian 11 Bullseye was used.

📢 Official: [Building PiKVM OS - PiKVM Handbook](https://docs.pikvm.org/building_os)

### 4.1 Install Dependencies (e.g. Docker)

```
apt install git make curl binutils
apt install docker.io
usermod -aG docker $USER

mkdir /root/pikvm
cd /root/pikvm
git clone --depth=1 https://github.com/pikvm/os
cd os
```

### 4.2 Create Configuration File

Now you need to create a the configuration file `config.mk` at `/root/pikvm/config.mk`. 

Do not use the default values for passwords. Instead, generate a random 16-character password using following command:

```
printf '%s\n' $(head /dev/urandom | LC_ALL=C tr -dc A-Za-z0-9 | head -c16)
```

⚠️ **This configuration file is only valid for a Raspberry Pi 4 using the HDMI to CSI-2 Module.**

```
# rpi4 for Raspberry Pi 4; rpi3 for Raspberry Pi 3; rpi2 for the version 2, zero2w for Zero2W
BOARD = rpi4

# Hardware configuration
PLATFORM = v2-hdmi

# Target hostname
HOSTNAME = kvm-srv1

# ru_RU, etc. UTF-8 only
LOCALE = en_US

# See /usr/share/zoneinfo
TIMEZONE = Europe/Berlin

# For SSH root user
ROOT_PASSWD = ...

# Web UI credentials: user=admin, password=<this>
WEBUI_ADMIN_PASSWD = ...

# IPMI credentials: user=admin, password=<this>
IPMI_ADMIN_PASSWD = ...

# SD card device
CARD = /dev/mmcblk0
```

