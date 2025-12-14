# Maintainer: Patrik Pira
pkgname=('pcoip-client' 'pcoip-client-clipboard')
pkgver=25.06.3
_ubuntuver=22.04
pkgrel=2
boostver=1.71.0
boostfilesuffix="${boostver}_${boostver}-6ubuntu6_amd64.deb"
_protobufver=23
pkgdesc="Teradici PCOIP client"
arch=('x86_64')
license=('custom:Teradici')
depends=('openssl-1.1' 'pcsclite' 'qt5-networkauth' 'qt5-declarative' 'qt5-quickcontrols' 'qt5-quickcontrols2' 'qt5-graphicaleffects' 'qt5-webengine' 'glfw' 'ffmpeg')
makedepends=('fakeroot' 'patchelf')
install=$pkgname.install
#options=(!strip)
source=("https://dl.teradici.com/DeAdBCiUYInHcSTy/pcoip-client/deb/ubuntu/pool/jammy/main/p/pc/pcoip-client_${pkgver}-${_ubuntuver}/pcoip-client_${pkgver}-${_ubuntuver}_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf23_3.12.4-1ubuntu7_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/h/hiredis/libhiredis0.14_0.14.1-2_amd64.deb"
)

sha256sums=('857f2ac896f48ce522b605b2746cb6cea2d0a2cceb3eabf8c880f2a31bddd858'
 '8c9942e9130ab7c343438b1b81603bdd86509d7e2a9cc877ae35a998dbf5e0a8'
 'eb382ba7f1955d111a3b6a70e465d1d8accf995106315b4b9562378c328b411f'
)

prepare() {
  cd "$srcdir"
  mkdir -p pcoip-client libprotobuf libhiredis
  bsdtar -C pcoip-client -xvf pcoip-client_${pkgver}-${_ubuntuver}_amd64.deb
  bsdtar -C libprotobuf -xvf libprotobuf23_3.12.4-1ubuntu7_amd64.deb
  bsdtar -C libhiredis -xvf libhiredis0.14_0.14.1-2_amd64.deb
}

package_pcoip-client() {
  tar -C "$pkgdir"/ -xvf "$srcdir"/pcoip-client/data.tar.gz

  rm -f "$pkgdir"/usr/lib/x86_64-linux-gnu/org.hp.pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
  rm -f "$pkgdir"/usr/sbin/pcoip-configure-kernel-networking
  rmdir "$pkgdir"/usr/sbin

  #dependencies
  tar -C "$pkgdir"/ -xvf "$srcdir"/libprotobuf/data.tar.zst \
   ./usr/lib/x86_64-linux-gnu/libprotobuf.so.23.0.4
  tar -C "$pkgdir"/ -xvf "$srcdir"/libhiredis/data.tar.zst \
   ./usr/lib/x86_64-linux-gnu/libhiredis.so.0.14

  mv "$pkgdir"/usr/lib/x86_64-linux-gnu/lib*.so* \
   "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/
  ln -s libprotobuf.so.23.0.4 \
   "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/libprotobuf.so.23

  ln -s . "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/lib

  mv "$pkgdir"/usr/bin/libFlxCore64.so.2019.04 "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/
  mv "$pkgdir"/usr/bin/libFlxComm64.so.2019.04 "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/
# rm -f "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/libav*
# rm -f "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/libFlxCo*
# rm -f "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/libglfw*
# rm -f "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/libswscale.so*
# rm -rf "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/wayland
# rm -rf "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/x11
# rm -rf "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/pkgconfig

  chmod +x "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/lib*so*  
#  patchelf --set-rpath /usr/lib/x86_64-linux-gnu/pcoip-client \
#   "$pkgdir"/usr/lib/x86_64-linux-gnu/pcoip-client/librdp-session.so

  # remove urlhandler as it collides with the dedicated urlhandler
  sed -i -e 's!MimeType=x-scheme-handler/pcoip;!!' "$pkgdir"/usr/share/applications/pcoip-client.desktop

  # set capabilities
  setcap "cap_setgid+p" "$pkgdir/usr/libexec/pcoip-client/pcoip-client"
  setcap "cap_setgid+i" "$pkgdir/usr/libexec/pcoip-client/usb-helper"
}

package_pcoip-client-clipboard() {
  pkgdesc="Teradici PCOIP client clipboard synchronization plugin"
  tar -C "$pkgdir"/ -xvf "$srcdir"/pcoip-client/data.tar.gz ./usr/lib/x86_64-linux-gnu/org.hp.pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
}
