# Maintainer: Weird Gumi <weirdgumi@tutamail.com>

_name=Catch2
pkgbase=catch2
pkgname=(catch2{,-doc})
pkgver=3.16.1
pkgrel=1
pkgdesc='A modern, C++-native, test framework for unit-tests, TDD and BDD'
arch=(x86_64 aarch64 riscv64 loongarch64)
url=https://github.com/catchorg/Catch2
license=(BSL-1.0)
depends=(llvm-libs musl)
makedepends=(cmake python)
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('d16bd1b8b2364918bd472cb216394acb93bde6784890df0d91bccfb3f28d777d')

build() {
  cmake -S "$_name-$pkgver" -B build \
    -DCMAKE_BUILD_TYPE=None \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DBUILD_SHARED_LIBS=ON \
    -DCATCH_DEVELOPMENT_BUILD=ON \
    -DCATCH_ENABLE_WERROR=OFF
  cmake --build build
}

check() {
  ctest --test-dir build --output-on-failure
}

package_catch2() {
  provides=(libCatch2.so libCatch2Main.so)

  DESTDIR="$pkgdir" cmake --install build
  _install_license_ "$_name-$pkgver/LICENSE.txt"

  cd "$pkgdir"
  _pick_ doc usr/share/doc
}

package_catch2-doc() {
  pkgdesc+=' (Documentation)'
  arch=(any)
  depends=()

  cp -r pkgs/doc/usr "$pkgdir"
}
