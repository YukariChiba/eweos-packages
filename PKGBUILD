# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Anatol Pomozov <anatol.pomozov@gmail.com>

pkgname=cmocka
pkgver=1.1.5
pkgrel=2
pkgdesc='Elegant unit testing framework for C with support for mock objects'
url='https://cmocka.org/'
arch=(x86_64 aarch64)
license=('Apache')
depends=('musl')
makedepends=('cmake')
source=("https://cmocka.org/files/1.1/cmocka-${pkgver}.tar.xz")
sha512sums=('cad7f04757183d004f6eaad39036fc0e24c5e0e987f80e85bc43bc66dba22389cb02b08e25531cc28a541d0a24a86b29be134a2d6fc339128e87d66952f502bd')

prepare()
{
  cd ${pkgname}-${pkgver}
  mkdir build
}

build()
{
  cd ${pkgname}-${pkgver}/build
  cmake .. \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCMAKE_BUILD_TYPE=Release \
    -DUNIT_TESTING=ON
  make
}

check()
{
  cd ${pkgname}-${pkgver}/build
  make test
}

package()
{
  cd ${pkgname}-${pkgver}/build
  make install DESTDIR="${pkgdir}"
}
