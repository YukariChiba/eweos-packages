# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-packaging
pkgver=26.4
pkgrel=1
pkgdesc="Core utilities for Python packages"
arch=('any')
url="https://github.com/pypa/packaging"
license=('Apache')
depends=('python')
makedepends=('python-build' 'python-installer' 'python-flit-core')
checkdepends=("python-pytest" "python-pretend" "python-tomli-w" "python-hypothesis")
source=("https://github.com/pypa/packaging/archive/$pkgver/$pkgname-$pkgver.tar.gz")
sha512sums=('563375fad8898080ac1afec4b9deede5bc822892101ba7029781220e0b103cce61fadc359561a0d79689aed464ca3777a7164e2459107cd54401974e29a2d411')

build() {
  cd packaging-$pkgver
  python -m build -nw
}

check() {
  cd packaging-$pkgver
  # muslinux != linux
  PYTHONPATH=src python -m pytest \
    --ignore=tests/test_tags.py \
    --deselect tests/test_manylinux.py::test_is_manylinux_compatible_old
}

package() {
  cd packaging-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
}
