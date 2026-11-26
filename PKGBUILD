# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=python-psutil
_pyname=${pkgname#*-}
pkgver=7.2.2
pkgrel=1
pkgdesc='Cross-platform lib for process and system monitoring in Python'
url='https://github.com/giampaolo/psutil'
arch=(x86_64 aarch64 riscv64 loongarch64)
license=(BSD-3-Clause)
depends=(python)
makedepends=(python-build python-installer python-setuptools python-wheel
	     linux-headers)
checkdepends=(python-pytest)
source=("https://github.com/giampaolo/psutil/archive/refs/tags/release-$pkgver.tar.gz")
sha256sums=('38f406bf21acc67e45f414b7980463b2e6e6270ba3616ffd41995d997078cbe6')

build () {
	cd $_pyname-release-$pkgver
	python -m build --wheel --no-isolation
}

package() {
	cd $_pyname-release-$pkgver
	python -m installer --destdir $pkgdir dist/*.whl
}
