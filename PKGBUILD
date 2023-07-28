# Maintainer: Evangelos Foutras <evangelos@foutrelis.com>
# Contributor: Anatol Pomozov <anatol.pomozov@gmail.com>
# Contributor: Gustavo Alvarez <sl1pkn07@gmail.com>
# Contributor: Alexandre Bique <bique.alexandre@gmail.com>

pkgname=re2
_re2ver=2022-06-01
pkgrel=1
epoch=1
pkgver=${_re2ver//-/}
pkgdesc="Fast, safe, thread-friendly regular expression engine"
arch=(x86_64 aarch64 riscv64)
url="https://github.com/google/re2"
license=('BSD')
depends=('llvm-libs')
source=(re2-$pkgver.tar.gz::https://github.com/google/re2/archive/$_re2ver.tar.gz)
sha256sums=('f89c61410a072e5cbcf8c27e3a778da7d6fd2f2b5b1445cd4f4508bee946ab0f')

build()
{
  cd $pkgname-$_re2ver
  make
}

check()
{
  cd $pkgname-$_re2ver
  make test
}

package()
{
  cd $pkgname-$_re2ver
  make prefix=/usr DESTDIR="$pkgdir" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
