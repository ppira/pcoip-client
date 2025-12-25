# pcoip-client (Arch Linux PKGBUILD)

Community packaging for **HP Anyware Client** (formerly *Teradici PCoIP Client*) on Arch Linux by repackaging the official Ubuntu `.deb`.

- This is **not** an official HP/Teradici project.
- The client is **proprietary**; you must comply with the upstream license/EULA.
- `x86_64` only.

## Packages

This PKGBUILD produces split packages:

- `pcoip-client`: the main GUI client (`/usr/bin/pcoip-client`)
- `pcoip-client-clipboard`: optional clipboard sync vchan plugin

## Install (build from this repo)

```bash
makepkg -si
```

## Notes

- The PKGBUILD fetches the upstream client `.deb` plus the Ubuntu `libprotobuf23` it expects for ABI compatibility.
- Main package depends on system Qt, X11/XCB, audio, and VA-API; optional VA-API drivers are surfaced via `optdepends`.
- A wrapper forces `QT_QPA_PLATFORM=xcb` and the bundled Wayland Qt platform plugins are removed (upstream Wayland build is broken against Arch Qt).
- The clipboard plugin now pulls in `graphicsmagick` and is patched to link against the Arch SONAME.
- Capabilities for the client and USB helper are baked into the package during build; if they get lost, re-apply them manually (see troubleshooting).
- The upstream `.desktop` file is patched to avoid registering the `pcoip://` URL handler (to prevent collisions with dedicated URL-handler packages).

## libva Driver

Intel
```bash
intel-media-driver
libva-intel-driver
```

AMD
```bash
libva-mesa-driver
```

NVIDIA
```bash
libva-nvidia-driver
```

## Troubleshooting

- **USB redirection not working / permission errors**
  - Re-apply capabilities:
    - `sudo setcap cap_setgid+p /usr/libexec/pcoip-client/pcoip-client`
    - `sudo setcap cap_setgid+i /usr/libexec/pcoip-client/usb-helper`
- **Missing shared libraries**
  - Check: `ldd /usr/bin/pcoip-client | rg 'not found'`
