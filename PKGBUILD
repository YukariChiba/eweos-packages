# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=pawprint
pkgver=0.1.0
pkgrel=3
pkgdesc="A substitution of systemd-tmpfiles"
url="https://github.com/eweOS/pawprint"
license=(MIT)
arch=(x86_64 aarch64 riscv64)
makedepends=(git)
source=(
  "$pkgname::git+$url.git#branch=main"
  "$pkgname.service"
)
sha256sums=('SKIP'
            'f93ee18de7c6f6426427a7ce7aa8632d85802fbc5a1178860f7ba26a262506eb')

build()
{
  cd $pkgname
  cc -o $pkgname $pkgname.c -DARCH=$arch
}

package()
{
  cd $pkgname
  install -D $pkgname $pkgdir/usr/bin/$pkgname
  install -d $pkgdir/etc/tmpfiles.d
  _dinit_install_services_ $srcdir/$pkgname.service
}
