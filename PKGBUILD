# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Dave Reisner <dreisner@archlinux.org>
# Contributor: Angel Velasquez <angvp@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: Andrea Scarpino <andrea@archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgname=libssh2
pkgver=1.10.0
pkgrel=1
pkgdesc="A library implementing the SSH2 protocol as defined by Internet Drafts"
url="https://www.libssh2.org/"
arch=(x86_64 aarch64)
license=('BSD')
depends=('openssl' 'zlib')
provides=('libssh2.so')
source=("https://www.libssh2.org/download/$pkgname-$pkgver.tar.gz")
sha256sums=('2d64e90f3ded394b91d3a2e774ca203a4179f69aebee03003e5a6fa621e41d51')

build()
{
  cd "$pkgname-$pkgver"

  ./configure --prefix=/usr
  make
}

check()
{
  make -C "$pkgname-$pkgver" check
}

package()
{
  cd "$pkgname-$pkgver"

  make DESTDIR="$pkgdir" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
