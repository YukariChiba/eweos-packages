# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=libqtxdg
pkgver=4.5.0
pkgrel=1
pkgdesc="Library providing freedesktop.org XDG specs implementations for Qt"
arch=("x86_64" "aarch64" "riscv64" "loongarch64")
url="https://github.com/lxqt/$pkgname"
license=("LGPL-2.1-or-later" "LGPL-2.1-only WITH Qt-LGPL-exception-1.1")
depends=("qt6-base" "qt6-svg")
makedepends=("cmake" "lxqt-build-tools" 'qt6-base-devel')
provides=("libQt6Xdg.so" "libQt6XdgIconLoader.so")
# 0001: Downstream, skip non-writable directory checks when running as root.
# The eweOS build container runs as root, where mode-based write checks do not
# fail. The test sets up its temporary directory before skipping so cleanup is safe.
source=(
  "https://github.com/lxqt/$pkgname/releases/download/$pkgver/$pkgname-$pkgver.tar.xz"
  "0001-tst-xdgdirs-skip-root.patch"
)
sha256sums=('64edfa2bc219366be099ed37115be9a440f53800974cbc967bca0f7080bca1e5'
            'a64ac4f942d01e9035de5cc97572fcfac2da5062c2f6f3d58ad488c9f5755a46')

prepare() {
  _patch_ "$pkgname-$pkgver"
}

build() {
  mkdir -p build
  cd build
  cmake "$srcdir/$pkgname-$pkgver" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DBUILD_TESTS=ON
  make
}

check() {
  cd build

  # The tests do not exercise Wayland-specific behavior, so use the offscreen
  # platform plugin instead of running a compositor in the build container.
  export QT_QPA_PLATFORM=offscreen
  ctest --output-on-failure
}

package() {
  cd build
  make DESTDIR="$pkgdir" install
  install -Dm644 "$srcdir/$pkgname-$pkgver"/{AUTHORS,COPYING,Digia-Qt-LGPL-Exception-1.1} \
    -t "$pkgdir"/usr/share/licenses/$pkgname
}
