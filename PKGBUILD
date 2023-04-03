# Maintainer: Aleksana QwQ <me@aleksana.moe>

pkgname=fribidi
pkgver=1.0.12
pkgrel=1
pkgdesc="A Free Implementation of the Unicode Bidirectional Algorithm"
url="https://github.com/fribidi/fribidi/"
arch=(x86_64 aarch64)
license=(LGPL)
depends=(musl)
makedepends=(meson)
provides=(libfribidi.so)
source=("https://github.com/fribidi/fribidi/releases/download/v1.0.12/fribidi-${pkgver}.tar.xz")
sha256sums=('0cd233f97fc8c67bb3ac27ce8440def5d3ffacf516765b91c2cc654498293495')

build()
{
  ewe-meson $pkgname-$pkgver build \
    -D docs=false
  meson compile -C build
}

check()
{
  meson test -C build --print-errorlogs
}

package()
{
  meson install -C build --destdir "$pkgdir"
}
