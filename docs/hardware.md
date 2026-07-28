# DakuOS hardware policy

## Wi-Fi – prefer fastest band

**Important limitation:** A Wi-Fi *client* cannot choose the channel the router uses. Channel planning is done by the access point. What DakuOS does:

1. Prefer **6 GHz** (Wi-Fi 6E / Wi-Fi 7) when the network offers it  
2. Else prefer **5 GHz** over 2.4 GHz  
3. Among APs with the same SSID, pick the BSSID with the best score (band bonus + signal)

There is **no standard consumer 7 GHz Wi-Fi band**. Wi-Fi 7 operates on 2.4 / 5 / 6 GHz. Higher generation + higher band is what “fastest available” means in practice.

Implementation:

- `config/includes.chroot/etc/NetworkManager/conf.d/00-dakuos-wifi.conf`
- `config/includes.chroot/etc/NetworkManager/dispatcher.d/10-dakuos-prefer-high-band`

Requires a Wi-Fi 6E/7 capable card and firmware (`firmware-iwlwifi`) — typical on Intel Core Ultra systems (e.g. BE200).

## 2-in-1 tablet mode + rotation

Packages:

- `iio-sensor-proxy` – accelerometer / orientation to the desktop  
- udev rules tag tablet-mode switches and IIO devices  
- `maliit-keyboard` – on-screen keyboard useful in tablet mode  

Plasma’s own rotation and tablet handling use these sensors when the chassis reports tablet mode (360° hinge / lid switch).

Fan and CPU temperature monitoring stay at desktop defaults; change them after install if you want.

## Intel Core Ultra 288V (Lunar Lake)

| Component | Package / service |
|-----------|-------------------|
| Microcode | `intel-microcode` |
| Thermal daemon | `thermald` |
| User power profiles (Performance / Balanced / Power Saver) | `power-profiles-daemon` |
| GPU / media | `mesa-vulkan-drivers`, `intel-media-va-driver-non-free` |
| Kernel | Latest Testing `linux-image-amd64` (7.0.x) |

Plasma’s battery/power applet talks to `power-profiles-daemon` so you can switch profiles without extra tools.

## SSD + boot speed

- Weekly `fstrim.timer` (TRIM) enabled  
- `noatime` policy documented for installed root filesystem  
- sysctl: lower swappiness, tuned dirty ratios for NVMe  
- GRUB timeout 2 seconds, `quiet splash`  
- Plymouth spinner until custom logo is provided  

## Branding

See [branding.md](branding.md). Debian logos are removed; drop your logo into `config/includes.chroot/usr/share/dakuos/branding/`.
