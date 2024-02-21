# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=hicolor-icon-theme
pkgver=0.17
pkgrel=1
pkgdesc="Freedesktop.org Hicolor icon theme"
arch=('any')
url="https://www.freedesktop.org/wiki/Software/icon-theme/"
license=('GPL2')
source=("https://icon-theme.freedesktop.org/releases/${pkgname}-${pkgver}.tar.xz")
sha256sums=('317484352271d18cbbcfac3868eab798d67fff1b8402e740baa6ff41d588a9d8')

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="${pkgdir}" install
}

