# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=opentimelineio
pkgver=0.18.1
pkgrel=1
pkgdesc='Open Source API and interchange format for editorial timeline information'
arch=(x86_64 aarch64 riscv64 loongarch64)
url='https://opentimeline.io/'
license=(Apache-2.0)
depends=(imath)
makedepends=(cmake
             'rapidjson>=1.1.0-5')
# 0001: Downstream, provide CursorStreamWrapper for RapidJSON 1.1.0
source=("opentimelineio-$pkgver.tar.gz::https://github.com/AcademySoftwareFoundation/OpenTimelineIO/archive/refs/tags/v$pkgver.tar.gz"
        0001-add-local-CursorStreamWrapper.patch)
sha256sums=('bcb516a43a962dac0cde3e1f9da634c1fd409915d499ff8f3ce6f738a4637d72'
            '9677532c5c8950050cc18c45c4195b27d927126974ae091eb8759f5b92b2f705')

prepare() {
  _patch_ "OpenTimelineIO-$pkgver"
}

build() {
  cmake -B build -S "OpenTimelineIO-$pkgver" \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=lib \
    -DCMAKE_BUILD_TYPE=RelWithDebInfo \
    -DOTIO_FIND_IMATH=ON \
    -DOTIO_FIND_RAPIDJSON=ON \
    -DOTIO_AUTOMATIC_SUBMODULES=OFF \
    -DOTIO_DEPENDENCIES_INSTALL=OFF
  cmake --build build
}

check() {
  ctest --test-dir build --output-on-failure
}

package() {
  cd "OpenTimelineIO-$pkgver"
  DESTDIR="$pkgdir" cmake --install "$srcdir/build"
  _install_license_ LICENSE.txt LICENSE.txt
  _install_license_ NOTICE.txt NOTICE.txt
}
