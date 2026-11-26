# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-jaraco.context
pkgver=6.1.2
pkgrel=1
pkgdesc="Context managers by jaraco"
url="https://github.com/jaraco/jaraco.context"
license=('MIT')
arch=('any')
depends=('python')
makedepends=('git' 'python-build' 'python-installer' 'python-wheel' 'python-setuptools-scm')
checkdepends=('python-pytest' 'python-portend')
source=("git+https://github.com/jaraco/jaraco.context.git#tag=v$pkgver")
sha512sums=('558b266e3924c3c9b379b30fff0d6ac247ae08d75fca1252afbe00f6ebdac6fa47f62fd22907b242206fcbd20ac47243e69068e54c73e5a04e83a69123906b7d')

prepare() {
  cd jaraco.context
  # Upstream replaced LICENSE with the unpackaged coherent.licensed build dependency.
  sed -i '/coherent.licensed/d' pyproject.toml
  git show v6.0.0:LICENSE > LICENSE
}

build() {
  cd jaraco.context
  python -m build -wn
}

check() {
  cd jaraco.context
  # Doctest requires the unpackaged `ensure_git` fixture.
  python -m pytest --deselect jaraco/context/__init__.py::jaraco.context.repo_context
}

package() {
  cd jaraco.context
  python -m installer -d "$pkgdir" dist/*.whl
  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname/
}
