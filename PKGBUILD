# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-dateutil
pkgver=4.0.0
pkgrel=1
pkgdesc="Provides powerful extensions to the standard datetime module"
arch=(any)
license=(BSD-3-Clause Apache-2.0)
url="https://github.com/dateutil/dateutil"
depends=(python-six tzdata)
makedepends=(python-build
             python-installer
             python-wheel
             python-hatchling
             python-hatch-vcs
             python-hatch-fancy-pypi-readme
             python-six git)
# FIXME: missing check dependencies
#checkdepends=(python-freezegun
#              python-hypothesis
#              python-pytest)
source=("git+$url.git#tag=$pkgver")
sha256sums=('c349804832ad0f832de3e82be937b872edce811a704e249480a877871550df0a')

prepare() {
  cd dateutil
}

build() {
  cd dateutil
  python -m build -wn
}

check() {
  cd dateutil
  # https://github.com/pytest-dev/pytest/issues/5678
  # PYTHONPATH=src pytest -W ignore::pytest.PytestUnknownMarkWarning .
}

package() {
  cd dateutil
  python -m installer -d "$pkgdir" dist/*.whl
  install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
}
