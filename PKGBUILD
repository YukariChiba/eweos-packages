# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=polkit
pkgver=124
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
url="https://gitlab.freedesktop.org/polkit/polkit"
arch=(x86_64 aarch64 riscv64)
license=(LGPL-2.0-or-later)
depends=(
  expat
  duktape
  glib
  pam
)
makedepends=(
  git
  gobject-introspection
  meson
  docbook-xsl
)
provides=(libpolkit-{agent,gobject}-1.so)
backup=(etc/pam.d/polkit-1)
source=(
  "git+https://gitlab.freedesktop.org/polkit/polkit.git#tag=$pkgver"
  0001-meson-Pass-polkitd_uid-to-meson_post_install.py.patch
)
sha256sums=('SKIP'
            '3f38c437a792accd2ae22e46f41460d23ba7f1e389deef10b7015cccae15ab0d')

prepare() {
  _patch_ $pkgname
}

build() {
  local meson_options=(
    -D examples=true
    -D man=true
    -D os_type=redhat
    -D polkitd_uid=102
    -D polkitd_user=polkitd
    -D session_tracking=ConsoleKit
    -D tests=true
  )

  ewe-meson polkit build "${meson_options[@]}"
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs -t 3
}

package() {
  meson install -C build --destdir "$pkgdir"
}
