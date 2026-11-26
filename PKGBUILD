# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=python-referencing
_pyname=${pkgname#*-}
_referencingsuite_commit=b74fd4535fed598519d23c8cd74e5e8c77489440
pkgver=0.37.0
pkgrel=1
pkgdesc='An implementation-agnostic implementation of JSON reference resolution'
url='https://referencing.readthedocs.io/'
arch=(any)
license=(MIT)
depends=(python python-attrs python-rpds-py)
makedepends=(python-build python-installer python-setuptools python-wheel
	     python-hatchling python-hatch-vcs git)
checkdepends=(python-pytest)
source=("https://github.com/python-jsonschema/referencing/archive/refs/tags/v$pkgver.tar.gz"
	"git+https://github.com/python-jsonschema/referencing-suite.git#commit=$_referencingsuite_commit")
sha256sums=('83541258d7e1c5b7e4507319b9c7e92b6aa7d538711f071fa02315de9a56e971'
            'c04946527a8c28b44e7b033e663f942a1baa444b1f45d37273074d02fdac4357')

build() {
	cd "$_pyname-$pkgver"
	SETUPTOOLS_SCM_PRETEND_VERSION="$pkgver" \
		python -m build --wheel --no-isolation
}

check() {
	cd "$_pyname-$pkgver"
	REFERENCING_SUITE="$srcdir/referencing-suite" pytest -vv
}

package() {
	cd "$_pyname-$pkgver"
	python -m installer --destdir "$pkgdir" dist/*.whl
}
