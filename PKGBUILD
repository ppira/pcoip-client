# Maintainer: Patrik Pira
pkgname=pcoip-client
pkgver=22.01.0
_ubuntuver=20.04
pkgrel=1
majorboostver=1.71
boostver=1.71.0
boostfilesuffix="${boostver}_${boostver}-6ubuntu11_amd64.deb"
_protobufver=17
pkgdesc="Teradici PCOIP client for x86_64 (64bit) Linux"
arch=('x86_64')
license=('custom:Teradici')
depends=('pcsclite' 'qt5-declarative' 'qt5-quickcontrols' 'qt5-webengine' 'glfw' 'ffmpeg')
makedepends=('fakeroot' 'patchelf')
install=$pkgname.install
#options=(!strip)
#source=("https://downloads.teradici.com/ubuntu/pool/non-free/p/pcoip-client/pcoip-client_${pkgver}-18.04_amd64.deb"
source=("https://dl.teradici.com/DeAdBCiUYInHcSTy/pcoip-client/deb/ubuntu/pool/focal/main/p/pc/pcoip-client_${pkgver}-${_ubuntuver}/pcoip-client_${pkgver}-${_ubuntuver}_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf17_3.6.1.3-2ubuntu5_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/h/hiredis/libhiredis0.14_0.14.1-2_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-system${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-thread${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-chrono${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-filesystem${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-regex${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${majorboostver}/libboost-serialization${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${majorboostver}/libboost-random${boostfilesuffix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${majorboostver}/libboost-container${boostfilesuffix}"
)

sha256sums=('SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
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

package() {
  tar -C $pkgdir/ -xvf $srcdir/pcoip-client/data.tar.gz

  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
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

  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libav*
  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libFlxCo*
  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libglfw*
  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libswscale.so*
  rm -rf $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/wayland
  rm -rf $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/x11
  rm -rf $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/pkgconfig

  chmod +x $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/lib*so*  
  patchelf --set-rpath /usr/lib/x86_64-linux-gnu/pcoip-client \
   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/librdp-session.so
}
