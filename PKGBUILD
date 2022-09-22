# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Allan McRae <allan@archlinux.org>
# Contributor: Jan de Groot <jgc@archlinux.org>

pkgname=gmp
pkgver=6.2.1
pkgrel=2
pkgdesc='A free library for arbitrary precision arithmetic'
arch=(x86_64)
url='https://gmplib.org/'
license=(LGPL3 GPL)
source=(https://gmplib.org/download/gmp/gmp-$pkgver.tar.lz)
md5sums=('SKIP')

build() {
  cd $pkgname-$pkgver

  ./configure --build=${CHOST} \
    --prefix=/usr \
    --enable-cxx \
    --enable-fat
  make
}

check() {
  cd $pkgname-$pkgver
  make check
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="${pkgdir}" install
}

