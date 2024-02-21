# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=xdg-desktop-portal
pkgver=1.18.2
pkgrel=1
pkgdesc="Desktop integration portals for sandboxed apps"
url="https://flatpak.github.io/xdg-desktop-portal/"
arch=(x86_64 aarch64 riscv64)
license=(LGPL)
depends=(
  glib
  json-glib
  pipewire
  fuse3
  gdk-pixbuf
  bubblewrap
)
makedepends=(
  git
  meson
)
optdepends=('xdg-desktop-portal-impl: Portal backends')
source=("git+https://github.com/flatpak/xdg-desktop-portal#tag=$pkgver")
sha256sums=('SKIP')

build() {
  local features=(
    -D flatpak-interfaces=disabled
    -D geoclue=disabled
    -D libportal=disabled
    -D systemd=disabled
    -D docbook-docs=disabled
    -D man-pages=disabled
    -D pytest=disabled
  )
  ewe-meson $pkgname build "${features[@]}"
  meson compile -C build
}

#check() {
#  meson test -C build --print-errorlogs
#}

package() {
  meson install -C build --destdir "$pkgdir"

  # remove systemd services
  rm -r $pkgdir/usr/lib/systemd || true
}
