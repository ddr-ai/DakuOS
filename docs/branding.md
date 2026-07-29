# DakuOS branding

Debian logos and trademark artwork are removed during the image build.

## Official logo

The fiery **DAKU** mark is the official logo. Assets live at:

```text
config/includes.chroot/usr/share/dakuos/branding/logo-boot.jpg.b64
config/includes.chroot/usr/share/dakuos/branding/logo-icon.jpg.b64
```

Hook `030-dakuos-branding.hook.chroot` decodes them and installs:

| Surface | Target |
|---------|--------|
| Boot splash (Plymouth) | `/usr/share/plymouth/themes/dakuos/` |
| Login (SDDM) | Breeze theme background |
| GRUB menu | `/boot/grub/dakuos-background.jpg` |
| Desktop wallpaper | `/usr/share/wallpapers/DakuOS/` |

## Replacing the logo

1. Decode: `base64 -d logo-boot.jpg.b64 > logo.jpg`
2. Edit / replace the image
3. Re-encode: `base64 -w0 logo.jpg > logo-boot.jpg.b64`
4. Rebuild the ISO
