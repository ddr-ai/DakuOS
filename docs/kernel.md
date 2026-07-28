# DakuOS kernel policy

## Default kernel

DakuOS uses the **latest Linux kernel from Debian Testing (Forky)**.

| Item | Value |
|------|--------|
| Distribution | Debian Testing (`forky`) |
| Metapackage | `linux-image-amd64` |
| Headers | `linux-headers-amd64` |
| Current Testing series | **7.0.x** (e.g. `7.0.10+deb14-amd64`) |

This is configured in:

- `auto/config` → `--linux-packages "linux-image linux-headers" --linux-flavours amd64`
- `config/package-lists/kernel.list.chroot`

Every ISO build pulls whatever version is newest in Testing at build time. No kernel version is hard-pinned, so the image stays current with Forky.

## Why Testing (not Unstable / Experimental)

- Testing has a delay gate and no open RC bugs of severity serious/critical before packages enter.
- Unstable and Experimental can ship broken intermediate kernels.
- 7.0.x in Testing is the newest *rolling-stable* line suitable for a daily-driver distro.

Experimental currently carries 7.2-rc kernels; those are intentionally **not** used by default.

## Custom kernel modifications

When you need a kernel tuned for specific hardware or features (e.g. extra drivers, different preemption model, stripped modules, custom config options):

1. Describe the requirements (hardware, features to enable/disable, performance goals).
2. We will add either:
   - a **custom kernel package** built from Debian kernel source with a DakuOS config fragment, or
   - a live-build hook that installs a pre-built custom `.deb` from a DakuOS package repo.

Until that is defined, DakuOS ships the stock Debian Testing `linux-image-amd64`.

## Checking the kernel on a built image

```bash
uname -r
apt-cache policy linux-image-amd64
```
