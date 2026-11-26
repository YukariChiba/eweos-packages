# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=python-requests
_pyname=${pkgname#*-}
pkgver=2.34.2
pkgrel=1
pkgdesc='An elegant and simple HTTP library for Python, built for human beings.'
url='https://requests.readthedocs.io'
arch=(any)
license=(Apache-2.0)
depends=(python ca-certificates python-charset-normalizer python-idna
	 python-urllib3 python-certifi)
optdepends=('python-chardet: alternative character encoding library'
	    'python-pysocks: SOCKS proxy support')
makedepends=(python-build python-installer python-setuptools python-wheel)
# checkdepends=(python-pytest python-pytest-httpbin python-trustme)
source=("https://github.com/psf/requests/archive/refs/tags/v$pkgver.tar.gz")
sha256sums=('d3c132d905099fa3468bb5cb273c2bdf5a7a92dce987c93b198820b3a7b57228')

build () {
	cd $_pyname-$pkgver
	python -m build --wheel --no-isolation
}

# missing python-pytest-httpbin python-trustme
# check() {
# 	cd $_pyname-$pkgver
#	pytest -v
# }

package() {
	cd $_pyname-$pkgver
	python -m installer --destdir $pkgdir dist/*.whl
	_install_license_ LICENSE
}
