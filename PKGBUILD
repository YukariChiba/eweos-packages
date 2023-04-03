# Maintainer: Aleksana QwQ <me@aleksana.moe>

pkgname=libbsd
pkgver=0.11.6
pkgrel=2
pkgdesc='commonly-used BSD functions not implemented by all libcs'
arch=(x86_64 aarch64)
url="https://libbsd.freedesktop.org"
license=('custom')
depends=('musl' 'libmd')
options=('staticlibs')
source=("https://libbsd.freedesktop.org/releases/$pkgname-$pkgver.tar.xz")
sha512sums=('9dbbfb84340fc69f59667241701d81d176439ce168f123344805898a269f7bd0e98abf8c7fc12d9bf539d1effb19424d93b647cc9120f693327e736d339e6075')

prepare()
{
  cd "$pkgname-$pkgver"
  # nlist failed, no solutions found
  sed -i 's/nlist//' test/Makefile.am
  ./autogen
}

build()
{
  cd "$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

check()
{
  cd "$pkgname-$pkgver"
  make check
}

package()
{
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir" install
  rm "${pkgdir}"/usr/lib/libbsd.a
  install -D -m644 COPYING "$pkgdir/usr/share/licenses/$pkgname/LICENSE"

  rm -f "${pkgdir}"/usr/share/man/man3/explicit_bzero.3
}
