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

## Installing from a live USB

The live image includes the **Calamares** graphical installer (branded as DakuOS).

1. Boot the ISO (USB or virtual machine) and choose the first GRUB entry (live session).
2. After Plasma starts you should get a **Welcome to DakuOS** dialog:
   - **Install DakuOS** — opens the installer immediately  
   - **Try without installing** — stays in the live session  
3. If you dismissed the dialog, install any of these ways:
   - Application menu → search **Install** or **DakuOS** → **Install DakuOS**
   - Desktop icon **Install DakuOS** (if desktop icons are enabled)
   - Terminal: `calamares-install-debian`
4. Follow the wizard: language → keyboard → disks → user → install.
5. Reboot when finished (remove the USB when prompted).

Calamares copies the live system to disk, installs GRUB, creates your user, and removes live-only packages (including the installer itself).

> Note: classic `debian-installer` is not on the image (`--debian-installer none`) because of package issues on current Debian Testing. Calamares is the supported install path.
>
> Plasma often hides desktop icons by default — that is why the welcome dialog and the application menu entry matter more than a Desktop file alone.

## Building the ISO

### GitHub Actions (recommended)

A workflow is provided at `.github/workflows/build-iso.yml`.

- **Manual run**: Go to the **Actions** tab → “Build DakuOS ISO” → **Run workflow**
- **Automatic**: Runs on pushes to `main` that change `auto/`, `config/`, or the workflow itself

The resulting ISO (and build log) is uploaded as a workflow artifact and kept for 14 days.

### Local build

```bash
# On a Debian Testing host or container (preferred)
sudo apt install live-build debootstrap squashfs-tools xorriso \
  isolinux syslinux-utils grub-pc-bin grub-efi-amd64-bin mtools dosfstools

git clone https://github.com/ddr-ai/DakuOS.git
cd DakuOS
chmod +x auto/config config/hooks/live/*.hook.chroot

./auto/config          # or: lb config
sudo lb build 2>&1 | tee build.log
```

The hybrid ISO will appear in the current directory (e.g. `live-image-amd64.hybrid.iso`).

## Current Status

- Vision and core decisions locked  
- Initial `live-build` configuration present  
- GitHub Actions ISO build workflow added  
- Successful hybrid ISO builds with branding  
- Calamares installer on the live desktop (Install DakuOS)

## License

To be decided (likely a free software license compatible with Debian).

---

DakuOS is developed by [ddr-ai](https://github.com/ddr-ai).
