# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-idna
pkgver=3.20
pkgrel=1
pkgdesc="Internationalized Domain Names in Applications (IDNA)"
arch=('any')
license=('BSD-3-Clause')
url="https://github.com/kjd/idna"
depends=('python')
makedepends=('python-build' 'python-installer' 'python-flit-core')
checkdepends=('python-pytest')
source=("https://github.com/kjd/idna/archive/v$pkgver/$pkgname-$pkgver.tar.gz")
sha512sums=('fd3afe8d531a68dde34d18f749765b6e5556aee22c0c2eaf42032ffbb588b833100dd9a7f85eb4e81ddba6d0be051a953d2573f9f98f08ed91c187cd2f8c6613')

build() {
   cd idna-$pkgver
   python -m build --no-isolation --wheel
}

check() {
   cd idna-$pkgver
   pytest -v
}

package() {
   cd idna-$pkgver
   python -m installer --destdir="$pkgdir" dist/*.whl
   _install_license_ LICENSE.md
}

