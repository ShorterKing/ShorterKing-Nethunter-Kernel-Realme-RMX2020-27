# ShorterKing NetHunter Kernel — realme C3 / Narzo 10A (RMX2020)

Custom **Kali NetHunter** kernel for the **realme C3 / realme Narzo 10A** (`RMX2020`, MediaTek **MT6768**) on **Android 13 / crDroid 13**.

Built to boot with the **internal Wi-Fi and Bluetooth fully working**, then stacked with penetration-testing features on top.

```
Kernel:  4.14.323-ShorterKing-Nethunter
Device:  realme C3 / Narzo 10A  (RMX2020 / RMX2027)
SoC:     MediaTek MT6768
ROM:     crDroid 13.0 (Android 13)
Base:    ArrowOS-Devices/android_kernel_realme_RMX2020
```

> For authorized security testing and education only. Flashing a custom kernel is at your own risk.

## Features

- ✅ Internal **Wi-Fi + Bluetooth** working
- 📶 **External USB Wi-Fi adapters** — many chipsets built in, plus out-of-tree Realtek drivers (auto-loaded)
- 🎯 **Monitor mode & packet injection**
- ⌨️ **HID / BadUSB** (DuckHunter)
- 🔌 **USB gadget arsenal** — RNDIS, NCM, ACM, Mass Storage, FunctionFS
- 🗄️ **System V IPC** — PostgreSQL / Metasploit `msfdb` work
- 🧱 **MITM / routing** — iptables + NAT, NFQUEUE, TPROXY, TUN, bridge, VLAN
- 📡 Full **Bluetooth stack** (RFCOMM, BNEP, HIDP, HCI USB/UART, VHCI)
- 🔗 USB serial (FTDI/PL2303/CH341/CP210x) and USB-Ethernet (AX8817x/AX88179/CDCEther/RTL8152)
- 🛰️ **RTL-SDR** — RTL2832U software-defined radio (`rtl_433`, ADS-B, gqrx) *(v1.1)*
- 🚗 **CAN bus / SocketCAN** — USB-CAN adapters for automotive work *(v1.1)*
- 🔐 **WireGuard** — in-kernel VPN module, auto-loaded *(v1.1)*
- 🔎 **On-device tracing** — kprobes / uprobes / ftrace for Frida & perf *(v1.1)*

## Supported Wi-Fi adapters

**Built in (`mac80211`, firmware embedded):** `ath9k_htc` (AR9271), `carl9170`, `ar5523`, `mt7601u`, `rt2800usb`, `rtl8187`, `rtl8192cu`, `zd1211rw`, `p54usb`, `mwifiex_usb`, `brcmfmac`, and more.

**Out-of-tree (shipped as auto-loading modules):** RTL8812AU/8814AU (`88XXau`), RTL8822BU (`88x2bu`), RTL8192EU (`8192eu`), RTL8188EU (`r8188eu`), RTL8723AU (`r8712u`).

## Download & flash

Download the flashable zip from the [**Releases**](../../releases) page, then in TWRP/recovery:

1. Back up your current `boot` partition.
2. Flash `nethunter-rmx2020-v1.1.zip`.
3. Reboot.

The zip flashes the kernel and installs the external Wi-Fi drivers as a systemless module that auto-loads at boot and shows up in `/system/lib/modules` for the NetHunter app.

## Build from source

```sh
export ARCH=arm64
# Proton Clang toolchain required
make O=out ARCH=arm64 nethunter_defconfig
make O=out ARCH=arm64 -j$(nproc) CC=clang
```
The kernel config is `arch/arm64/configs/nethunter_defconfig`.

## Credits

- [ArrowOS-Devices](https://github.com/ArrowOS-Devices/android_kernel_realme_RMX2020) — base kernel source
- [osm0sis/AnyKernel3](https://github.com/osm0sis/AnyKernel3) — flasher
- [aircrack-ng/rtl8812au](https://github.com/aircrack-ng/rtl8812au), [morrownr](https://github.com/morrownr), and the Mange `rtl8192eu` driver
- [Kali NetHunter](https://www.kali.org/docs/nethunter/)

## License

GPL-2.0 (Linux kernel). See [`COPYING`](COPYING).
