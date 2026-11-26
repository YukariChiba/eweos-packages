# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=python-imagesize
_pyname=imagesize_py
pkgver=2.0.1
pkgrel=1
pkgdesc='Module for analyzing image headers and returns image size or DIP.'
url='https://github.com/shibukawa/imagesize_py'
arch=(any)
license=(MIT)
depends=(python)
makedepends=(python-build python-installer python-setuptools python-wheel)
checkdepends=(python-pytest)
source=("https://github.com/shibukawa/imagesize_py/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('0fdd765d9768fb0b5d3005a925e7a76b0a5a965b3c4a3228226cbe99c3f24c31')

prepare() {
	# the link now 404....
	rm $_pyname-$pkgver/test/test_get_filelike.py
}

build () {
	cd $_pyname-$pkgver
	python -m build --wheel --no-isolation
}

check() {
	cd $_pyname-$pkgver
	pytest -v
}

package() {
	cd $_pyname-$pkgver
	python -m installer --destdir $pkgdir dist/*.whl
	_install_license_ LICENSE.rst
}
