# Maintainer: Patrik Pira
pkgname=('pcoip-client' 'pcoip-client-clipboard')
pkgver=25.10.2
_ubuntuver=22.04
pkgrel=3
url='https://anyware.hp.com/'
arch=('x86_64')
license=('custom:Teradici')
depends=(
  'alsa-lib>=1.0.17'
  'dbus>=1.9.14'
  'expat>=2.1'
  'fontconfig>=2.12.6'
  'freetype2>=2.9.1'
  'glib2>=2.26.0'
  'krb5>=1.17'
  'libcap>=2.10'
  'libdrm>=2.4.38'
  'libglvnd'
  'libpng>=1.6.2' # Undeclared in .deb file
  'libpulse>=0.99.1'
  'libva>=2.1.0'
  'libx11>=1.2.99.901'
  'libxcb>=1.7.5'
  'libxext'
  'libxi>=1.2.99.4'
  'libxkbcommon-x11>=0.5.0'
  'mesa>=21.1.0'
  'nspr>=4.9'
  'nss>=3.30'
  'pcsclite>=1.3.3'
  'systemd>=183'
  'xcb-util>=0.4.0'
  'xcb-util-image>=0.2.1'
  'xcb-util-keysyms>=0.4.0'
  'xcb-util-renderutil'
  'xcb-util-wm>=0.4.1'
  'zlib'
  # gcc-libs provides libatomic1, libc6, libgcc-s1, libstdc++6 (base)
)
optdepends=(
  'intel-media-driver: VA-API for newer Intel GPUs'
  'libva-intel-driver: VA-API for older Intel GPUs'
  'libva-mesa-driver: VA-API for Intel/AMD GPUs via Mesa'
  'libva-nvidia-driver: VA-API for NVIDIA GPUs (proprietary driver required)'
)
makedepends=('fakeroot' 'patchelf')
source=(
  "https://dl.anyware.hp.com/DeAdBCiUYInHcSTy/pcoip-client/deb/ubuntu/pool/jammy/main/p/pc/pcoip-client_${pkgver}-${_ubuntuver}/pcoip-client_${pkgver}-${_ubuntuver}_amd64.deb"
  "http://se.archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf23_3.12.4-1ubuntu7_amd64.deb"
)

sha256sums=(
  '9138b29fe4e8352b0a472dd8b33ed9889b420fed4711aec0e9759ff74311d6e5'
  '8c9942e9130ab7c343438b1b81603bdd86509d7e2a9cc877ae35a998dbf5e0a8'
)

prepare() {
  cd "$srcdir"
  mkdir -p pcoip-client libprotobuf
  # Unpack upstream client and the Ubuntu runtime dep we vendor.
  bsdtar -C pcoip-client -xf pcoip-client_${pkgver}-${_ubuntuver}_amd64.deb
  bsdtar -C libprotobuf -xf libprotobuf23_3.12.4-1ubuntu7_amd64.deb
}

package_pcoip-client() {
  pkgdesc="Teradici PCOIP client"
  local vendor_root="$pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client"

  tar -C "$pkgdir"/ -xf "$srcdir"/pcoip-client/data.tar.gz

  # Upstream ships /usr/sbin but Arch uses a filesystem-provided /usr/sbin -> /usr/bin symlink.
  install -d "$pkgdir/usr/bin"
  mv "$pkgdir"/usr/sbin/pcoip-configure-kernel-networking "$pkgdir"/usr/bin/
  rm -rf "$pkgdir"/usr/sbin

  # Force X11/XCB because we drop the broken Wayland Qt plugin.
  rm "$pkgdir"/usr/bin/pcoip-client
  cat <<'EOF' > "$pkgdir"/usr/bin/pcoip-client
#!/bin/sh
export QT_QPA_PLATFORM="${QT_QPA_PLATFORM:-xcb}"
exec /usr/libexec/pcoip-client/pcoip-client "$@"
EOF
  chmod +x "$pkgdir/usr/bin/pcoip-client"

  # Remove unused upstream directories not needed on Arch.
  rm -rf \
    "$pkgdir"/usr/lib/x86_64-linux-gnu/org.hp.pcoip-client \
    "$pkgdir"/var \
    "$pkgdir"/usr/share/icons/hicolor/128x128 \
    "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/pkgconfig \
    "$pkgdir"/usr/share/man

  # Drop Wayland Qt platform plugins that fail with system libQt6WaylandClient.
  rm -f "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/plugins/platforms/libqwayland-*.so

  # Bundle Ubuntu protobuf for ABI compatibility.
  tar -C "$pkgdir"/ -xf "$srcdir"/libprotobuf/data.tar.zst \
    ./usr/lib/x86_64-linux-gnu/libprotobuf.so.23.0.4

  # Keep vendor libs contained and provide the expected SONAME symlink.
  mv "$pkgdir"/usr/lib/x86_64-linux-gnu/lib*.so* "$vendor_root"/
  ln -s libprotobuf.so.23.0.4 "$vendor_root"/libprotobuf.so.23

  # Qt looks for a sibling lib/ directory.
  ln -s . "$vendor_root"/lib

  chmod +x "$vendor_root"/lib*so*

  # remove urlhandler as it collides with the dedicated urlhandler
  sed -i -e 's!MimeType=x-scheme-handler/pcoip;!!' "$pkgdir"/usr/share/applications/pcoip-client.desktop

  # set capabilities
  setcap "cap_setgid+p" "$pkgdir/usr/libexec/pcoip-client/pcoip-client"
  setcap "cap_setgid+i" "$pkgdir/usr/libexec/pcoip-client/usb-helper"
}

package_pcoip-client-clipboard() {
  pkgdesc="Teradici PCOIP client clipboard synchronization plugin"
  depends=('pcoip-client' 'graphicsmagick>=1.3.26')
  install=

  tar -C "$pkgdir"/ -xf "$srcdir"/pcoip-client/data.tar.gz \
    ./usr/lib/x86_64-linux-gnu/org.hp.pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
  chmod +x "$pkgdir"/usr/lib/x86_64-linux-gnu/org.hp.pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
  patchelf --replace-needed libGraphicsMagick++-Q16.so.12 libGraphicsMagick++.so.12 \
    "$pkgdir"/usr/lib/x86_64-linux-gnu/org.hp.pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
}
