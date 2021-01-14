# Maintainer: Patrik Pira
pkgname=pcoip-client
pkgver=21.01.0
pkgrel=1
boostmajorver=1.65.1
boostver=1.65.1
boostfilesuffix="${boostver}_${boostver}+dfsg-0ubuntu5_amd64.deb"
_protobufver=10
pkgdesc="Teradici PCOIP client for x86_64 (64bit) Linux"
arch=('x86_64')
license=('custom:Teradici')
depends=('pcsclite' 'qt5-declarative' 'qt5-quickcontrols')
makedepends=('fakeroot')
#options=(!strip)
source=("https://downloads.teradici.com/ubuntu/pool/non-free/p/pcoip-client/pcoip-client_${pkgver}-18.04_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf10_3.0.0-9.1ubuntu1_amd64.deb"
#"http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${boostmajorver}/libboost-system${boostfilesuffix}"
#"http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${boostmajorver}/libboost-thread${boostfilesuffix}"
#"http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${boostmajorver}/libboost-chrono${boostfilesuffix}"
#"http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${boostmajorver}/libboost-filesystem${boostfilesuffix}"
#"http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${boostmajorver}/libboost-regex${boostfilesuffix}"
#"http://se.archive.ubuntu.com/ubuntu/pool/main/b/boost${boostmajorver}/libboost-serialization${boostfilesuffix}"
)
sha256sums=('SKIP'
 'SKIP'
# 'SKIP'
# 'SKIP'
# 'SKIP'
# 'SKIP'
# 'SKIP'
# 'SKIP'
)

prepare() {
  cd $srcdir
  mkdir -p pcoip-client libprotobuf libboost-system libboost-thread \
   libboost-chrono libboost-regex libboost-filesystem libboost-serialization
  bsdtar -C pcoip-client -xvf pcoip-client_${pkgver}-18.04_amd64.deb
  bsdtar -C libprotobuf -xvf libprotobuf10_3.0.0-9.1ubuntu1_amd64.deb
#  bsdtar -C libboost-system -xvf libboost-system${boostfilesuffix}
#  bsdtar -C libboost-thread -xvf libboost-thread${boostfilesuffix}
#  bsdtar -C libboost-chrono -xvf libboost-chrono${boostfilesuffix}
#  bsdtar -C libboost-filesystem -xvf libboost-filesystem${boostfilesuffix}
#  bsdtar -C libboost-regex -xvf libboost-regex${boostfilesuffix}
#  bsdtar -C libboost-serialization -xvf libboost-serialization${boostfilesuffix}
}

package() {
  tar -C $pkgdir/ -xvf $srcdir/pcoip-client/data.tar.gz

  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/vchan_plugins/libvchan-plugin-clipboard.so
  rm -f $pkgdir/usr/sbin/pcoip-configure-kernel-networking
  rmdir $pkgdir/usr/sbin

  #dependencies
  tar -C $pkgdir/ -xvf $srcdir/libprotobuf/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libprotobuf.so.10.0.0
#  tar -C $pkgdir/ -xvf $srcdir/libboost-system/data.tar.xz \
#   ./usr/lib/x86_64-linux-gnu/libboost_system.so.${boostver}
#  tar -C $pkgdir/ -xvf $srcdir/libboost-thread/data.tar.xz \
#   ./usr/lib/x86_64-linux-gnu/libboost_thread.so.${boostver}
#  tar -C $pkgdir/ -xvf $srcdir/libboost-chrono/data.tar.xz \
#   ./usr/lib/x86_64-linux-gnu/libboost_chrono.so.${boostver}
#  tar -C $pkgdir/ -xvf $srcdir/libboost-filesystem/data.tar.xz \
#   ./usr/lib/x86_64-linux-gnu/libboost_filesystem.so.${boostver}
#  tar -C $pkgdir/ -xvf $srcdir/libboost-regex/data.tar.xz \
#   ./usr/lib/x86_64-linux-gnu/libboost_regex.so.${boostver}
#  tar -C $pkgdir/ -xvf $srcdir/libboost-serialization/data.tar.xz \
#   ./usr/lib/x86_64-linux-gnu/libboost_serialization.so.${boostver}

  mv $pkgdir/usr/lib/x86_64-linux-gnu/lib*.so* \
   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/
  ln -s libprotobuf.so.10.0.0 \
   $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/libprotobuf.so.10
  ln -s . $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/lib

  chmod +x $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/lib*so*  
}
