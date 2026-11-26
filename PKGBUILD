# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-snowballstemmer
pkgver=3.1.1
pkgrel=1
arch=('any')
pkgdesc="Snowball stemming library collection for Python"
url='https://snowballstem.org'
license=('BSD')
depends=('python')
optdepends=('python-pystemmer: for improved performance')
makedepends=('python-setuptools')
source=("https://pypi.python.org/packages/source/s/snowballstemmer/snowballstemmer-$pkgver.tar.gz")
sha512sums=('a36320c5c21b91137b6924025edac292891d3141a12cfe84fb1ee44f19980eeb35494bebf6c8cb9879c9633e06e27aa73f850157fbc074e926713ad47368b269')

build() {
  cd "$srcdir"/snowballstemmer-$pkgver
  python setup.py build
}

check() {
  cd "$srcdir"/snowballstemmer-$pkgver/src
  PYTHONPATH=. python sample/testapp.py english "what's this"
}

package() {
  cd "$srcdir"/snowballstemmer-$pkgver
  python setup.py install --root="$pkgdir" --optimize=1

  install -Dm644 COPYING "$pkgdir"/usr/share/licenses/$pkgname/COPYING
}
