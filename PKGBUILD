# Maintainer: Daniel Isenmann <daniel [at] archlinux.org>
# Contributor: dorphell <dorphell@gmx.net>

pkgname=gc
pkgver=8.2.2
pkgrel=1
pkgdesc="A garbage collector for C and C++"
arch=('x86_64')
url="https://www.hboehm.info/gc/"
license=('GPL')
depends=('llvm-libs')
source=(https://github.com/ivmai/bdwgc/releases/download/v${pkgver}/${pkgname}-${pkgver}.tar.gz)
sha512sums=('SKIP')

build() {
  cd ${pkgname}-${pkgver}
  ./configure --prefix=/usr \
	      --enable-cplusplus \
	      --disable-static
  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool
  make
}

check() {
  cd ${pkgname}-${pkgver}
  make check
}

package() {
  cd ${pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" install
  sed 's|GC_MALLOC 1L|gc 3|g' doc/gc.man |
    install -Dm644 /dev/stdin "${pkgdir}/usr/share/man/man3/gc.3"
}
