# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-chardet
pkgver=7.2.0
pkgrel=1
arch=('any')
url="https://github.com/chardet/chardet"
license=('LGPL')
depends=('python')
pkgdesc="Python3 module for character encoding auto-detection"
makedepends=('python-build' 'python-installer' 'python-hatchling' 'git')
checkdepends=('python-pytest')
source=("git+$url.git#tag=$pkgver")
sha256sums=('SKIP')

prepare() {
  cd chardet
  # Modify pyproject.toml to remove hatch-vcs dependency
  sed -i 's/, "hatch-vcs"//' pyproject.toml
  sed -i 's/"hatch-vcs", //' pyproject.toml
  # Remove [tool.hatch.version] section
  sed -i '/^\[tool.hatch.version\]/,/^\[/{/^\[tool.hatch.version\]/!d}' pyproject.toml
  # Remove [tool.hatch.build.hooks.vcs] section
  sed -i '/^\[tool.hatch.build.hooks.vcs\]/,/^\[/{/^\[tool.hatch.build.hooks.vcs\]/!d}' pyproject.toml
  # Remove version dynamic and set static version
  sed -i 's/dynamic = \["version"\]/version = "'$pkgver'"/' pyproject.toml
}

build() {
  cd chardet
  # Create _version.py manually
  echo "__version__ = '$pkgver'" > src/chardet/_version.py
  python -m build --wheel --no-isolation
}

check() {
  cd chardet
  PYTHONPATH="$PWD/src" python -m pytest -m "not benchmark"
}

package() {
  cd chardet
  python -m installer --destdir="$pkgdir" dist/*.whl
}

