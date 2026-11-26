# Maintainer: Yukari Chiba <i@0x7f.cc>

_pkgname=poetry-core
pkgname=python-${_pkgname}
pkgver=2.5.0
pkgrel=1
pkgdesc='Poetry PEP 517 Build Backend & Core Utilities'
arch=(any)
url="https://github.com/python-poetry/${_pkgname}"
license=(MIT)
groups=(python-build-backend)
_pydeps=(fastjsonschema
         lark-parser
         packaging)
depends=(
  python
  python-fastjsonschema
  python-lark-parser
  python-packaging
)
makedepends=(python-build python-installer)
#FIXME: missing check depends
#checkdepends=(git
#              python-pytest
#              python-pytest-mock
#              python-setuptools
#              python-tomli-w
#              python-virtualenv)
_archive="$_pkgname-$pkgver"
# 0001: Downstream, use system packages instead of bundled copies
source=("$url/archive/$pkgver/$_archive.tar.gz"
        "0001-devendor.patch")
sha256sums=('e5a6fa94749ba460c56898d2b9649e3779b9f20f225d75be2fdff0ec43a3449d'
            'df315d516bdf22250b0386324c82ce5b386fe9eff67985b92317da91e375ea7b')

prepare() {
	_patch_ "$_archive"
	rm -rv "$_archive/src/poetry/core/_vendor"
}

build() {
	cd "$_archive"
	python -m build -wn
}

check() {
	cd "$_archive"
	export PYTHONPATH="$PWD/src"
	#FIXME: missing check depends
	# only works inside git repositories
	#pytest \
	#	-k 'not test_default_with_excluded_data and not test_default_src_with_excluded_data'
}

package() {
	cd "$_archive"
	python -m installer -d "$pkgdir" dist/*.whl
	install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
}
