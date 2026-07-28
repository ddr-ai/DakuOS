# DakuOS

**DakuOS** is a custom Linux distribution built on the Debian core.

## Vision

DakuOS uses Debian as its foundation and aims for a **rolling release model with a meaningful level of stability**.

- **Core**: Pure Debian packages and infrastructure  
- **Release model**: Continuous updates (rolling) rather than fixed point releases  
- **Stability goal**: More reliable and usable day-to-day than pure Debian Unstable (Sid), while staying significantly newer than Debian Stable

## Locked Decisions

| Component              | Choice                                      |
|------------------------|---------------------------------------------|
| Base distribution      | Debian Testing (**Forky**)                  |
| Desktop environment    | **KDE Plasma** (default)                    |
| Browser                | **Firefox ESR**                             |
| Terminal               | **Ghostty**                                 |
| Code editor            | **Visual Studio Code** (official Microsoft) |
| Installation philosophy| Hardware-aware: only install firmware, drivers and tools needed for the detected system (no bloat) |

### Hardware-aware installation

The installer uses udev / modalias detection (via Debian Installer’s `hw-detect`) together with custom scripts so that only the firmware, drivers and related packages required by the actual hardware are installed. Unused firmware packages are not left behind.

## Included Applications

1. **Ghostty** – modern GPU-accelerated terminal  
2. **Visual Studio Code** – official Microsoft build  
3. **Firefox ESR** – Extended Support Release for stability on a Testing base

## Technical Direction

| Aspect                | Approach                                           |
|-----------------------|----------------------------------------------------|
| Base                  | Debian Testing (Forky)                             |
| Package sources       | Testing + Security + non-free-firmware             |
| Live images           | Built with `live-build`                            |
| Desktop               | `task-kde-desktop` + Plasma                        |
| Extra applications    | Ghostty (third-party), VS Code (Microsoft repo), Firefox ESR |
| Firmware handling     | Detected and installed only as needed              |
| Custom packages       | Small DakuOS repository (planned)                  |

## Current Status

- Vision and core decisions locked  
- Initial `live-build` configuration being added  
- First ISO builds coming next

## Building

See the `config/` and `auto/` directories (coming online now).

```bash
# On a Debian Testing host or container
sudo apt install live-build
cd DakuOS
lb config          # or ./auto/config
sudo lb build
```

## License

To be decided (likely a free software license compatible with Debian).

---

DakuOS is developed by [ddr-ai](https://github.com/ddr-ai).
