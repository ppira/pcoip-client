# Maintainer: Patrik Pira
pkgname=pcoip-client
pkgver=20.04.0
pkgrel=1
boostmajorver=1.67
boostver=1.67.0
boostfilesufix="${boostver}_${boostver}-17ubuntu8_amd64.deb"
_protobufver=10
pkgdesc="Teradici PCOIP client for x86_64 (64bit) Linux"
arch=('x86_64')
license=('custom:Teradici')
depends=('glew2.0' 'glfw')
makedepends=('fakeroot')
#options=(!strip)
source=("https://downloads.teradici.com/ubuntu/pool/non-free/p/pcoip-client/pcoip-client_${pkgver}-18.04_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf10_3.0.0-9.1ubuntu1_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${boostmajorver}/libboost-system${boostfilesufix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${boostmajorver}/libboost-thread${boostfilesufix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${boostmajorver}/libboost-chrono${boostfilesufix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${boostmajorver}/libboost-filesystem${boostfilesufix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${boostmajorver}/libboost-regex${boostfilesufix}"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost${boostmajorver}/libboost-serialization${boostfilesufix}")
sha256sums=('SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP')

prepare() {
  cd $srcdir
  mkdir -p pcoip-client libprotobuf libboost-system libboost-thread \
   libboost-chrono libboost-regex libboost-filesystem libboost-serialization
  bsdtar -C pcoip-client -xvf pcoip-client_${pkgver}-18.04_amd64.deb
  bsdtar -C libprotobuf -xvf libprotobuf10_3.0.0-9.1ubuntu1_amd64.deb
  bsdtar -C libboost-system -xvf libboost-system${boostfilesufix}
  bsdtar -C libboost-thread -xvf libboost-thread${boostfilesufix}
  bsdtar -C libboost-chrono -xvf libboost-chrono${boostfilesufix}
  bsdtar -C libboost-filesystem -xvf libboost-filesystem${boostfilesufix}
  bsdtar -C libboost-regex -xvf libboost-regex${boostfilesufix}
  bsdtar -C libboost-serialization -xvf libboost-serialization${boostfilesufix}
}

package() {
  tar -C $pkgdir/ -xvf $srcdir/pcoip-client/data.tar.gz

  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
  rm -f $pkgdir/usr/sbin/pcoip-configure-kernel-networking
  rmdir $pkgdir/usr/sbin

  #dependencies
  tar -C $pkgdir/ -xvf $srcdir/libprotobuf/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libprotobuf.so.10.0.0
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

#  mv $pkgdir/usr/lib/x86_64-linux-gnu/lib*.so* \
#   $pkgdir/opt/pcoip-client/lib/
  mv $pkgdir/usr/lib/x86_64-linux-gnu/lib*.so* \
   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/
#  ln -s libprotobuf.so.10.0.0 \
#   $pkgdir/opt/pcoip-client/lib/libprotobuf.so.10
  ln -s libprotobuf.so.10.0.0 \
   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libprotobuf.so.10
  ln -s . $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/lib

#  chmod +x $pkgdir/opt/pcoip-client/lib/lib*so*  
  chmod +x $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/lib*so*  
  
#  rmdir $pkgdir/usr/lib/x86_64-linux-gnu
#  rmdir $pkgdir/usr/lib
}
