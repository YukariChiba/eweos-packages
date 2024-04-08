# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname='cmd-polkit'
pkgver=r8.069d66b
pkgrel=1
pkgdesc="Command line tool for custom polkit agent UIs"
arch=('x86_64' 'aarch64' 'riscv64')
url="https://github.com/OmarCastro/cmd-polkit"
license=('MIT')
depends=('glib' 'json-glib' 'polkit' 'gtk3')
makedepends=('git' 'meson')
source=("${pkgname}::git+https://github.com/OmarCastro/cmd-polkit.git")
md5sums=('SKIP')

pkgver() {
  cd "${pkgname}"
  printf "r%s.%s" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

build() {
  ewe-meson $pkgname build
  meson compile -C build
}

package() {
  meson install -C build --destdir "$pkgdir"
  install -Dm644 "$pkgname/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
