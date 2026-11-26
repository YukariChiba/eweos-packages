# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-cairo
pkgver=1.29.2
pkgrel=1
pkgdesc="Python bindings for the cairo graphics library"
url="https://pycairo.readthedocs.io/en/latest/"
arch=(x86_64 aarch64 riscv64 loongarch64)
license=(LGPL2.1 MPL)
depends=(cairo python)
makedepends=(meson)
checkdepends=(python-pytest)
source=(https://github.com/pygobject/pycairo/releases/download/v$pkgver/pycairo-$pkgver.tar.gz)
sha256sums=('3e69fff74fe64f5ba2dfa31f67c6bdf26413342574047437d2ac520d35e9a489')

build() {
  ewe-meson pycairo-$pkgver build
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir="$pkgdir"

  # compile Python bytecode
  python -m compileall -d /usr/lib "$pkgdir/usr/lib"
  python -O -m compileall -d /usr/lib "$pkgdir/usr/lib"
}
