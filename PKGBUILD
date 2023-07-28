# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=pango
pkgver=1.50.12
pkgrel=1
pkgdesc="A library for layout and rendering of text"
url="https://www.pango.org/"
arch=(x86_64 aarch64 riscv64)
license=(LGPL)
depends=(cairo glib fribidi harfbuzz)
makedepends=(meson gobject-introspection)
source=("https://download.gnome.org/sources/$pkgname/1.50/$pkgname-$pkgver.tar.xz")
sha256sums=('caef96d27bbe792a6be92727c73468d832b13da57c8071ef79b9df69ee058fe3')

build() {
  ewe-meson $pkgname-$pkgver build \
    -D libthai=disabled \
    -D xft=disabled
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
}

