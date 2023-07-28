# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Christian Rebischke <Chris.Rebischke@archlinux.org>
# Contributor: Massimiliano Torromeo <massimiliano.torromeo@gmail.com>
# Contributor: Anatol Pomozov <anatol.pomozov gmail>
# Contributor: RunningDroid <runningdroid AT zoho.com>
# Contributor: Xiao-Long Chen <chenxiaolong@cxl.epac.to>

pkgname=gflags
pkgver=2.2.2
pkgrel=4
pkgdesc='C++ Library for commandline flag processing'
arch=(x86_64 aarch64 riscv64)
url='https://github.com/schuhschuh/gflags'
license=('BSD')
depends=('llvm-libs')
makedepends=('cmake')
source=("${pkgname}-${pkgver}.tar.gz::https://github.com/schuhschuh/gflags/archive/v${pkgver}.tar.gz")
sha512sums=('98c4703aab24e81fe551f7831ab797fb73d0f7dfc516addb34b9ff6d0914e5fd398207889b1ae555bac039537b1d4677067dae403b64903577078d99c1bdb447')
options=('!lto' 'staticlibs')

build()
{
  cd "gflags-${pkgver}"
  cmake . \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_BUILD_TYPE=Release \
    -DREGISTER_INSTALL_PREFIX=OFF \
    -DBUILD_SHARED_LIBS=ON \
    -DBUILD_STATIC_LIBS=ON \
    -DBUILD_TESTING=ON
  make
}

check()
{
  cd "gflags-${pkgver}"
  make test
}

package()
{
  cd "gflags-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -D -m644 COPYING.txt "${pkgdir}"/usr/share/licenses/${pkgname}/COPYING.txt
}
