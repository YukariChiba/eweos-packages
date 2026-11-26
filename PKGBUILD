# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-pycparser
pkgver=3.12
pkgrel=1
pkgdesc='C parser and AST generator written in Python'
url='https://github.com/eliben/pycparser'
depends=('python')
makedepends=('python-build' 'python-installer' 'python-setuptools')
arch=('any')
license=('BSD')
# 0001: Downstream, use clang-cpp instead of the unavailable GNU cpp
source=(
  "$pkgname-$pkgver.tar.gz::https://github.com/eliben/pycparser/archive/release_v$pkgver.tar.gz"
  0001-clang-cpp.patch
)
sha256sums=('3c8a08f01bbbd1b1a13e1c2029329b441e958479bf040ca7a8d2864b9ce7006c'
            '29db38eef38553947239873ae3dbba2e6c87cfdd56919f59f0b3660e781222b3')

prepare() {
  _patch_ pycparser-release_v$pkgver
}

build() {
  cd "$srcdir"/pycparser-release_v$pkgver
  python -m build --wheel --no-isolation
}

check() {
  cd "$srcdir"/pycparser-release_v$pkgver
  PYTHONPATH="$PWD" python -m unittest discover
}

package() {
  cd pycparser-release_v$pkgver

  python -m installer --destdir "$pkgdir" dist/*.whl
  install -Dm644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
