# Maintainer: Patrik Pira
pkgname=pcoip-client
pkgver=19.08.2
pkgrel=4
_boostver=1.65.1
_protobufver=10
pkgdesc="Teradici PCOIP client for x86_64 (64bit) Linux"
arch=('x86_64')
license=('custom:Teradici')
depends=('glew2.0' 'glfw' 'icu63')
makedepends=('fakeroot')
#options=(!strip)
source=("https://downloads.teradici.com/ubuntu/pool/non-free/p/pcoip-client/pcoip-client_${pkgver}-18.04_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf10_3.0.0-9.1ubuntu1_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost1.65.1/libboost-system1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost1.65.1/libboost-thread1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost1.65.1//libboost-chrono1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost1.65.1/libboost-filesystem1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost1.65.1/libboost-regex1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb"
 "http://se.archive.ubuntu.com/ubuntu/pool/universe/b/boost1.65.1/libboost-serialization1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb")
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
  bsdtar -C libboost-system -xvf libboost-system1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb
  bsdtar -C libboost-thread -xvf libboost-thread1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb
  bsdtar -C libboost-chrono -xvf libboost-chrono1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb
  bsdtar -C libboost-filesystem -xvf libboost-filesystem1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb
  bsdtar -C libboost-regex -xvf libboost-regex1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb
  bsdtar -C libboost-serialization -xvf libboost-serialization1.65.1_1.65.1+dfsg-0ubuntu11_amd64.deb
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
   ./usr/lib/x86_64-linux-gnu/libboost_system.so.1.65.1
  tar -C $pkgdir/ -xvf $srcdir/libboost-thread/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_thread.so.1.65.1
  tar -C $pkgdir/ -xvf $srcdir/libboost-chrono/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_chrono.so.1.65.1
  tar -C $pkgdir/ -xvf $srcdir/libboost-filesystem/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_filesystem.so.1.65.1
  tar -C $pkgdir/ -xvf $srcdir/libboost-regex/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_regex.so.1.65.1
  tar -C $pkgdir/ -xvf $srcdir/libboost-serialization/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_serialization.so.1.65.1

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
