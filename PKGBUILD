# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=cmake
_major_minor=3.25
pkgver="${_major_minor}.1"
pkgrel=1
pkgdesc='The CMake toolsuite for building, testing and packaging software.'
arch=('x86_64' 'aarch64')
url='https://cmake.org'
license=('GPL2')

source=(
  "${url}/files/v${_major_minor}/${pkgname}-${pkgver}.tar.gz"
)
sha256sums=('1c511d09516af493694ed9baf13c55947a36389674d657a2d5e0ccedc6b291d8')

build()
{
  cd ${pkgname}-${pkgver}
  ./bootstrap --prefix=/usr
  make
}

package()
{
  cd ${pkgname}-${pkgver}
  make DESTDIR="${pkgdir}" install
}
