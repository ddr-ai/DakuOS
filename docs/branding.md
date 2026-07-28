# DakuOS branding

Debian logos, trademark images, and default distributor artwork are removed from the live image during build.

## Where your logo goes

Place your logo files in the repository under:

```text
config/includes.chroot/usr/share/dakuos/branding/
```

| File | Purpose | Recommended size |
|------|---------|------------------|
| `logo.png` | General logo (login, menus) | 512×512 PNG, transparent |
| `logo-boot.png` | Plymouth splash (boot screen) | 1920×1080 or 2560×1440 PNG |
| `logo-login.png` | SDDM login screen background / watermark | 1920×1080 PNG |
| `logo-grub.png` | GRUB menu background | 1920×1080 PNG |

After you upload these files into the repo (or drop them into that path before a local build), a follow-up hook will wire them into:

1. **Plymouth** – image shown while the kernel and services start  
2. **SDDM** – login screen  
3. **GRUB** – boot menu background  
4. **Plasma** – application menu / about dialog (optional)

## Current state

- Debian branding files are deleted in `020-dakuos-services.hook.chroot`
- Plymouth uses the neutral `spinner` theme until a custom theme is added
- `GRUB_DISTRIBUTOR` is set to `DakuOS`
- Directory `/usr/share/dakuos/branding/` is created and ready for your assets

## Next step for you

Upload your logo image(s). Once they are in the repo under the path above, say so and the Plymouth + SDDM + GRUB themes will be connected to those files automatically.
