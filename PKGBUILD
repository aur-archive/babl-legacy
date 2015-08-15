pkgname=babl-legacy
_pkgname=babl
pkgver=0.1.6
pkgrel=3
pkgdesc="Babl is Dynamic, any to any, pixel format conversion library, legacy version of 0.1.6"
arch=('i686' 'x86_64')
url="http://gegl.org/babl/"
license=('LGPL3')
depends=('glibc' 'gobject-introspection')
options=('!libtool' '!makeflags')
conflicts=('babl')
provides=('babl')
source=(ftp://ftp.gimp.org/pub/babl/${pkgver%.*}/${_pkgname}-${pkgver}.tar.bz2)

md5sums=('dc960981a5ec5330fc1c177be9f59068')

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  sed -i -e '/--library=babl-$(BABL_API_VERSION)/a\\t\t--identifier-prefix= --symbol-prefix=babl\\' babl/Makefile.{am,in}
  sed -i -e 's/--library=babl-$(BABL_API_VERSION)/--library=libbabl-0.1.la/' babl/Makefile.{am,in}

  #./configure --prefix=/usr --program-suffix=legacy
  ./configure --prefix=/usr  --enable-introspection --program-suffix=legacy

  make
}

check() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make check
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
}
