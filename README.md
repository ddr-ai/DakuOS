# DakuOS

**DakuOS** is a custom Linux distribution built on the Debian core.

## Vision

DakuOS uses Debian as its foundation and aims for a **rolling release model with a meaningful level of stability**.

- **Core**: Pure Debian packages and infrastructure  
- **Release model**: Continuous updates (rolling) rather than fixed point releases  
- **Stability goal**: More reliable and usable day-to-day than pure Debian Unstable (Sid), while staying significantly newer than Debian Stable

### Technical Direction

The recommended baseline is **Debian Testing (Forky)**.

| Aspect              | Approach                                      |
|---------------------|-----------------------------------------------|
| Base distribution   | Debian Testing (Forky)                        |
| Package sources     | Testing + Security                            |
| Live images         | Built with `live-build` targeting Testing     |
| Stability tools     | Optional package pinning / hold profiles      |
| Custom packages     | Small DakuOS repository (future)              |
| Non-free firmware   | Included by default for hardware support      |

This gives users a continuously updated system while avoiding the highest breakage risk of pure Sid. Critical components (kernel, glibc, systemd, etc.) can later be protected with pinning or local freezes if needed.

Alternative paths that remain open:
- Sid-based with strong curation and pinning
- Hybrid (Stable core + selective Testing/Backports)

## Current Status

Early stage. Repository and vision defined. Live-build configuration and initial ISO builds are next.

## Building

(Coming soon — live-build configuration for Debian Testing will be added here.)

## License

To be decided (likely a free software license compatible with Debian).

---

DakuOS is developed by [ddr-ai](https://github.com/ddr-ai).
