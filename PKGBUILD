# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=giflib
pkgver=6.1.2
pkgrel=1
pkgdesc='Library for reading and writing gif images'
url='http://giflib.sourceforge.net/'
arch=(x86_64 aarch64 riscv64 loongarch64)
license=('MIT')
provides=('libgif.so')
makedepends=('xmlto' 'docbook-xml' 'docbook-xsl')
source=(https://downloads.sourceforge.net/project/giflib/giflib-6.x/${pkgname}-${pkgver}.tar.gz)
sha512sums=('523cf2a9941c6ddb903bf5ec22ecbf5a283c9470c1c85229360ab4137227a9e4a64b799e3ff0ca1f9f3b9de0fafe197a43fccd3c043239e76561f7b5ede59193')
options=(!zipman)

prepare() {
  cd ${pkgname}-${pkgver}
  # FIXME: imagemagick
  sed -i 's|convert $^ -resize 50x50 $@|cp $^ $@|' doc/Makefile
  # fix busybox head command
  sed -i 's/--bytes=-20/-c -20/' tests/makefile
}

build() {
  cd ${pkgname}-${pkgver}
  make
}

check() {
  cd ${pkgname}-${pkgver}
  make check
}

package() {
  cd ${pkgname}-${pkgver}
  make PREFIX=/usr DESTDIR="${pkgdir}" install
  install -Dm 644 COPYING -t "${pkgdir}/usr/share/licenses/${pkgname}"
}
