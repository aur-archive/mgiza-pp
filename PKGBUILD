# Maintainer: Filip Graliński <filipg@amu.edu.pl>
pkgname=mgiza-pp
pkgver=0.7.3
pkgrel=2
pkgdesc='A statical machine translation toolkit used to train word alignment models'
arch=('i686' 'x86_64')
url='https://code.google.com/p/giza-pp/'
license=('GPL2')
makedepends=(boost boost-libs gcc make)
depends=(python)
install=
source=("http://downloads.sourceforge.net/project/mgizapp/mgizapp-$pkgver.tgz")
md5sums=('deec1b021f2612be6edd78aca23ef418')

build() {
  cd "${srcdir}/mgizapp"

  rm CMakeCache.txt

  sed -i 's|set(Boost_USE_STATIC_LIBS        ON)|set(Boost_USE_STATIC_LIBS        OFF)|' CMakeLists.txt
  sed -i 's|FIND_PACKAGE( Boost 1.41 COMPONENTS thread)|FIND_PACKAGE( Boost 1.41 COMPONENTS thread system)|' CMakeLists.txt

  cmake . -DCMAKE_INSTALL_PREFIX=/usr -DBoost_USE_STATIC_LIBS=OFF

  make
}

package() {
  cd "${srcdir}/mgizapp"
  make DESTDIR="$pkgdir" install
  # conflict with giza-pp
  rm "${pkgdir}/usr/bin/mkcls"

  # move scripts to /usr/bin
  rm "${pkgdir}/usr/scripts/run.sh"
  cp ${pkgdir}/usr/scripts/* "${pkgdir}/usr/bin/"
  rm -rf "${pkgdir}/usr/scripts/"
  chmod a+rx ${pkgdir}/usr/bin/*.pl ${pkgdir}/usr/bin/*.sh ${pkgdir}/usr/bin/*.py
}
