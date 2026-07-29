# DakuOS branding

Debian logos and trademark artwork are stripped during the image build.

## Official logo

The fiery **DAKU** mark is the official logo.

### Recommended: drop the JPEG into the repo

1. Save your logo image as `logo-boot.jpg` (black background works best).
2. Upload it on GitHub to:

```text
config/includes.chroot/usr/share/dakuos/branding/logo-boot.jpg
```

   Use **Add file → Upload files** in that folder on GitHub.

3. Rebuild the ISO. The branding hook wires it to:

| Surface | Where it appears |
|---------|------------------|
| **Plymouth** | Boot splash while the system starts |
| **SDDM** | Login screen background |
| **GRUB** | Boot menu background |
| **Plasma** | DakuOS wallpaper |

### Alternate: base64 assets

- `logo-boot.jpg.b64` (or ordered `.part00`, `.part01`, … files)
- `logo-icon.jpg.b64` (smaller icon; already present in the repo)

Hook `030-dakuos-branding.hook.chroot` decodes these at build time.

## Current status

- Debian branding removed
- `GRUB_DISTRIBUTOR=DakuOS`
- Icon asset present
- **Upload full-quality `logo-boot.jpg` for the best boot and login splash**
