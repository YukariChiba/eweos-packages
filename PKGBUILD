# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=python-pyelftools
pkgver=0.33
pkgrel=1
pkgdesc='Parsing ELF and DWARF in Python.'
url='https://github.com/eliben/pyelftools'
arch=(any)
license=("custom:Public Domain")
depends=(python)
makedepends=(python-setuptools python-build python-installer python-wheel)
checkdepends=(python-pytest)
source=("https://github.com/eliben/pyelftools/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('5507d69b42ac7211e5db57b42f427376b2cf3e3ab9a72b9239f4fc243566869d')

build () {
	cd pyelftools-$pkgver
	python -m build --wheel --no-isolation
}

check() {
	cd pyelftools-$pkgver
	# needs python-utils
	# pytest
}

package() {
	cd pyelftools-$pkgver
	python -m installer --destdir=$pkgdir dist/*.whl
}
