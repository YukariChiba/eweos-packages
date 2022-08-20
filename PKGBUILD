# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=musl
pkgver=1.2.2
pkgrel=1
pkgdesc='An implementation of the C/POSIX standard library.'
arch=(x86_64)
url='https://musl.libc.org'
license=(LGPL BSD)
groups=(base-devel)
depends=()
makedepends=()
provides=(ld-musl-$(arch).so.1 libc.so)
options=()

source=(
    "http://www.etalabs.net/musl/releases/${pkgname[0]}-${pkgver}.tar.gz"
)
sha256sums=(
    'SKIP'
)

build() {
    cd $pkgname-$pkgver
    ./configure --prefix=/usr --syslibdir=/usr/lib
    make
}

package() {
    cd $pkgname-$pkgver
	make DESTDIR=${pkgdir} install
    install -d "${pkgdir}"/usr/bin
    ln -sf /usr/lib/libc.so "${pkgdir}"/usr/bin/ldd
}


