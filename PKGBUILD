# Maintainer: Patrik Pira
pkgname=pcoip-client
pkgver=3.8.1
pkgrel=1
_boostver=1.65.1
_protobufver=10
pkgdesc="Teradici PCOIP client for x86_64 (64bit) Linux"
arch=('x86_64')
license=('custom:Teradici')
#depends=('')
makedepends=('fakeroot')
#options=(!strip)
source=("https://downloads.teradici.com/ubuntu/pool/non-free/p/pcoip-client/pcoip-client_${pkgver}.18.04_amd64.deb"
 "http://launchpadlibrarian.net/362656392/libprotobuf10_3.0.0-9.1ubuntu1_amd64.deb"
 "http://launchpadlibrarian.net/359703399/libboost-system1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb"
 "http://launchpadlibrarian.net/359703401/libboost-thread1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb"
 "http://launchpadlibrarian.net/359703369/libboost-chrono1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb"
 "http://launchpadlibrarian.net/359703377/libboost-filesystem1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb"
 "http://launchpadlibrarian.net/359703395/libboost-serialization1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb")
sha256sums=('SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP'
 'SKIP')

prepare() {
  cd $srcdir
  mkdir -p pcoip-client libprotobuf libboost-system libboost-thread \
   libboost-chrono libboost-filesystem libboost-serialization
  bsdtar -C pcoip-client -xvf pcoip-client_${pkgver}.18.04_amd64.deb
  bsdtar -C libprotobuf -xvf libprotobuf10_3.0.0-9.1ubuntu1_amd64.deb
  bsdtar -C libboost-system -xvf libboost-system1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb
  bsdtar -C libboost-thread -xvf libboost-thread1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb
  bsdtar -C libboost-chrono -xvf libboost-chrono1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb
  bsdtar -C libboost-filesystem -xvf libboost-filesystem1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb
  bsdtar -C libboost-serialization -xvf libboost-serialization1.65.1_1.65.1+dfsg-0ubuntu5_amd64.deb
}

package() {
  tar -C $pkgdir/ -xvf $srcdir/pcoip-client/data.tar.gz

  rm -f $pkgdir/usr/lib/x86_64-linux-gnu/pcoip-client/vchan-plugins/libvchan-plugin-clipboard.so
  rm -f $pkgdir/usr/share/sbin/pcoip-configure-kernel-networking
  rmdir $pkgdir/usr/share/sbin

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
  tar -C $pkgdir/ -xvf $srcdir/libboost-serialization/data.tar.xz \
   ./usr/lib/x86_64-linux-gnu/libboost_serialization.so.1.65.1

  mv $pkgdir/usr/lib/x86_64-linux-gnu/lib*.so* \
   $pkgdir/opt/pcoip-client/lib/
  ln -s libprotobuf.so.10.0.0 \
   $pkgdir/opt/pcoip-client/lib/libprotobuf.so.10

  chmod +x $pkgdir/opt/pcoip-client/lib/lib*so*  
  
  rmdir $pkgdir/usr/lib/x86_64-linux-gnu
  rmdir $pkgdir/usr/lib
}
