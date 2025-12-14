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

- The PKGBUILD fetches the upstream client `.deb` plus a couple of runtime libraries used for compatibility on Arch.
- You may need `openssl-1.1` from the AUR (depending on your distro/repo set).
- Capabilities are applied on install via `pcoip-client.install` (used for USB redirection helpers).
- The upstream `.desktop` file is patched to avoid registering the `pcoip://` URL handler (to prevent collisions with dedicated URL-handler packages).

## Troubleshooting

- **USB redirection not working / permission errors**
  - Re-apply capabilities:
    - `sudo setcap cap_setgid+p /usr/libexec/pcoip-client/pcoip-client`
    - `sudo setcap cap_setgid+i /usr/libexec/pcoip-client/usb-helper`
- **Missing shared libraries**
  - Check: `ldd /usr/bin/pcoip-client | rg 'not found'`