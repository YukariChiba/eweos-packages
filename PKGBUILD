# Maintainer: Yukari Chiba <i@0x7f.cc>

_name=roman-numerals
pkgname=python-roman-numerals-py
pkgver=4.1.0
pkgrel=1
pkgdesc='Manipulate well-formed Roman numerals'
arch=(any)
url=https://github.com/AA-Turner/roman-numerals/tree/master/python
license=('0BSD OR CC0-1.0')
depends=(python)
makedepends=(
  git
  python-build
  python-flit-core
  python-installer
)
checkdepends=(python-pytest)
source=("git+https://github.com/AA-Turner/roman-numerals.git#tag=v$pkgver")
sha256sums=('6075c056a7847890069562694281857290789d73f2089c03385f5fa571d6e1c3')

prepare() {
  cd $_name
  cp LICENCE.rst python/
}

build() {
  cd $_name/python
  python -m build --wheel --skip-dependency-check --no-isolation
}

check() {
  cd $_name/python
  # Upstream passes enumerate() to parametrize; ignored until it is fixed for pytest 9.
  pytest -W ignore::pytest.PytestRemovedIn10Warning
}

package() {
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir"/usr/share/licenses/$pkgname
  ln -s "$site_packages"/roman_numerals_py-$pkgver.dist-info/licenses/LICENCE.rst \
    "$pkgdir"/usr/share/licenses/$pkgname/LICENCE.rst

  cd $_name/python
  python -m installer --destdir="$pkgdir" dist/*.whl
}

