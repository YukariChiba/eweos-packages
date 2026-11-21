# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=libaccounts-glib
pkgver=1.27
pkgrel=1
pkgdesc='Glib-based client library for accessing the online accounts database'
arch=(x86_64 aarch64 riscv64 loongarch64)
url='https://gitlab.com/accounts-sso/libaccounts-glib'
license=(LGPL-2.1-or-later)
depends=(
  glib2
  libxml2
  sqlite
)
makedepends=(
  check
  gobject-introspection
  gtk-doc
  meson
  vala
)
checkdepends=(dbus)
# 0001: Downstream, skip read-only tests when running as root
# chmod-based permission checks cannot make the database read-only for root,
# and eweOS builds run as root in the container.
source=("https://gitlab.com/accounts-sso/libaccounts-glib/-/archive/VERSION_$pkgver/libaccounts-glib-VERSION_$pkgver.tar.gz"
        "0001-skip-read-only-tests-as-root.patch")
sha256sums=('a8407a5897a2e425ea1aa955ecf88485dd2fd417919de275b27c781a5d0637a5'
            'f9cf6c0c6e147c9ad444f2565b13a74eba80a857b677d7969b6e2ef1fdc87b6d')

prepare() {
  _patch_ "$pkgname-VERSION_$pkgver"
}

build() {
  ewe-meson "$pkgname-VERSION_$pkgver" build
  meson compile -C build
}

check() {
  dbus-run-session -- meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"
  _install_license_ "$srcdir/$pkgname-VERSION_$pkgver/COPYING"
}
