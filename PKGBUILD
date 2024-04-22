# Maintainer: Yukari Chiba <i@0x7f.cc>
# Contributor: Aleksana QwQ <me@aleksana.moe>

pkgname=tree
pkgver=2.1.1
pkgrel=1
pkgdesc="A directory listing program displaying a depth indented list of files"
arch=(x86_64 aarch64 riscv64)
url="http://mama.indstate.edu/users/ice/tree/"
license=('GPL')
depends=('musl')
source=("https://gitlab.com/OldManProgrammer/unix-tree/-/archive/${pkgver}/unix-tree-${pkgver}.tar.gz")
sha512sums=('997d20c5508d3eba026e9d621a4da2b3b0bf111d272bb7d705a9a0819d430887061e234f0a00ac3102c43413ef716c1371ee0620b8460fbd523d4a3790940a29')

prepare()
{
  cd "unix-tree-${pkgver}"
  sed -i -e '/^CFLAGS/d' -e '/^LDFLAGS/d' -e '/^CC=/d' Makefile
}

build()
{
  cd "unix-tree-${pkgver}"
  make
}

package()
{
  cd "unix-tree-${pkgver}"
  make PREFIX="${pkgdir}/usr" MANDIR="${pkgdir}/usr/share/man" install
}
