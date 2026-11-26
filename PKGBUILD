# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=python-decorator
pkgver=5.3.2
pkgrel=1
pkgdesc='Decorators for Humans.'
url='https://github.com/micheles/decorator'
arch=(any)
license=(BSD-2-Clause)
depends=(python)
makedepends=(python-build python-installer python-wheel python-setuptools)
source=("https://github.com/micheles/decorator/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('7cc5d75ab78d3bd6f0335d21f57d43c3e193ad113e9eb4c967465259ec3b6474')

build () {
	cd "decorator-$pkgver"
	python -m build --wheel --no-isolation
}

check() {
	cd "decorator-$pkgver"
	PYTHONPATH="$PWD/src" python tests/test.py -vv
}

package() {
	cd "decorator-$pkgver"
	python -m installer --destdir "$pkgdir" dist/*.whl
	_install_license_ LICENSE.txt
}
