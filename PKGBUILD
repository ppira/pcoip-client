# Maintainer: Patrik Pira
pkgname=('pcoip-client' 'pcoip-client-clipboard')
pkgver=24.03.2
_ubuntuver=20.04
pkgrel=1
majorboostver=1.71
boostver=1.71.0
boostfilesuffix="${boostver}_${boostver}-6ubuntu6_amd64.deb"
_protobufver=17
pkgdesc="Teradici PCOIP client"
arch=('x86_64')
license=('custom:Teradici')
depends=('openssl-1.1' 'pcsclite' 'qt5-networkauth' 'qt5-declarative' 'qt5-quickcontrols' 'qt5-quickcontrols2' 'qt5-graphicaleffects' 'qt5-webengine' 'glfw' 'ffmpeg')
makedepends=('fakeroot' 'patchelf')
install=$pkgname.install
#options=(!strip)
source=("https://dl.teradici.com/DeAdBCiUYInHcSTy/pcoip-client/deb/ubuntu/pool/focal/main/p/pc/pcoip-client_${pkgver}-${_ubuntuver}/pcoip-client_${pkgver}-${_ubuntuver}_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf17_3.6.1.3-2ubuntu5_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/h/hiredis/libhiredis0.14_0.14.1-2_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-system${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-thread${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-chrono${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-filesystem${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${majorboostver}/libboost-regex${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-serialization${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${majorboostver}/libboost-random${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${majorboostver}/libboost-container${boostfilesuffix}"
)

sha256sums=('1158ad1f23ed2898a09b3ad3ab38760218dbf3b946c8976a5ad6571fdf3e3017'
 'b78b3d507dd2e70eeef31a703232980401d8f65b10db731b56deb44965482753'
 'eb382ba7f1955d111a3b6a70e465d1d8accf995106315b4b9562378c328b411f'
 '7d4e150855855a2788481f319f4cd9515f526f8fcbf7038a98441d68a8c4c4c1'
 '707045c56ef0141a77f449eed92eca741660ea1857b00a38db228e6038e0ac92'
 '4af58d4155189517f447300ee4535cb4db1351cb55802e28cec8c1f13ac108e6'
 '6793184cc2b8df0da401fdbe78fbf57ac598438177a6af163f99f9f1c14f9eb8'
 '7160fc29e33b7b191a618ae4b3ae0bc82c30ad5f38d00b82dc6362c9e954e377'
 '29a885e9b1353b1bb69c6d067909c689af86c02bf3a108db1b9d56e9cc63343c'
 'b5e9691cc94d42b5241293f6ad5bc5438201ed88979520e5604b779cb4da14fa'
 '992c307928860db9ff7c663c61da1f5545a13ffaa2329a8e111b248138235727'
)

prepare() {
  cd $srcdir
  mkdir -p pcoip-client libprotobuf libhiredis libboost-system libboost-thread \
   libboost-chrono libboost-regex libboost-filesystem libboost-serialization \
   libboost-random libboost-container
  bsdtar -C pcoip-client -xvf pcoip-client_${pkgver}-${_ubuntuver}_amd64.deb
  bsdtar -C libprotobuf -xvf libprotobuf17_3.6.1.3-2ubuntu5_amd64.deb
  bsdtar -C libhiredis -xvf libhiredis0.14_0.14.1-2_amd64.deb
  bsdtar -C libboost-system -xvf libboost-system${boostfilesuffix}
  bsdtar -C libboost-thread -xvf libboost-thread${boostfilesuffix}
  bsdtar -C libboost-chrono -xvf libboost-chrono${boostfilesuffix}
  bsdtar -C libboost-filesystem -xvf libboost-filesystem${boostfilesuffix}
  bsdtar -C libboost-regex -xvf libboost-regex${boostfilesuffix}
  bsdtar -C libboost-serialization -xvf libboost-serialization${boostfilesuffix}
  bsdtar -C libboost-random -xvf libboost-random${boostfilesuffix}
  bsdtar -C libboost-container -xvf libboost-container${boostfilesuffix}
}

package_pcoip-client() {
  tar -C $pkgdir/ -xvf $srcdir/pcoip-client/data.tar.gz

  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/org.hp.pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
  rm -f $pkgdir/usr/sbin/pcoip-configure-kernel-networking
  rmdir $pkgdir/usr/sbin

  #dependencies
  tar -C $pkgdir/ -xvf $srcdir/libprotobuf/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libprotobuf.so.17.0.0
  tar -C $pkgdir/ -xvf $srcdir/libhiredis/data.tar.zst \
   ./usr/lib/x86_64-linux-gnu/libhiredis.so.0.14
  tar -C $pkgdir/ -xvf $srcdir/libboost-system/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_system.so.${boostver}
  tar -C $pkgdir/ -xvf $srcdir/libboost-thread/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_thread.so.${boostver}
  tar -C $pkgdir/ -xvf $srcdir/libboost-chrono/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_chrono.so.${boostver}
  tar -C $pkgdir/ -xvf $srcdir/libboost-filesystem/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_filesystem.so.${boostver}
  tar -C $pkgdir/ -xvf $srcdir/libboost-regex/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_regex.so.${boostver}
  tar -C $pkgdir/ -xvf $srcdir/libboost-serialization/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_serialization.so.${boostver}
  tar -C $pkgdir/ -xvf $srcdir/libboost-random/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_random.so.${boostver}
  tar -C $pkgdir/ -xvf $srcdir/libboost-container/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_container.so.${boostver}

  mv $pkgdir/usr/lib/x86_64-linux-gnu/lib*.so* \
   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/
  ln -s libprotobuf.so.17.0.0 \
   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libprotobuf.so.17

  ln -s . $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/lib

  mv $pkgdir/usr/bin/libFlxCore64.so.2019.04 $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/
  mv $pkgdir/usr/bin/libFlxComm64.so.2019.04 $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/
# rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libav*
# rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libFlxCo*
# rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libglfw*
# rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libswscale.so*
# rm -rf $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/wayland
# rm -rf $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/x11
# rm -rf $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/pkgconfig

  chmod +x $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/lib*so*  
#  patchelf --set-rpath /usr/lib/x86_64-linux-gnu/pcoip-client \
#   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/librdp-session.so

  # remove urlhandler as it collides with the dedicated urlhandler
  sed -i -e 's!MimeType=x-scheme-handler/pcoip;!!' $pkgdir/usr/share/applications/pcoip-client.desktop
}

package_pcoip-client-clipboard() {
  pkgdesc="Teradici PCOIP client clipboard synchronization plugin"
  tar -C $pkgdir/ -xvf $srcdir/pcoip-client/data.tar.gz ./usr/lib/x86_64-linux-gnu/org.hp.pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
}
