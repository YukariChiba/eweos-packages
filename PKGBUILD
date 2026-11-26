# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-markdown
pkgver=3.11.4
pkgrel=1
pkgdesc="Python implementation of John Gruber's Markdown"
arch=('any')
url='https://python-markdown.github.io/'
license=('BSD-3-Clause')
depends=('python')
makedepends=('git' 'python-build' 'python-installer' 'python-setuptools' 'python-wheel')
optdepends=('python-yaml: parse Python in YAML metadata')
checkdepends=('python-yaml')
source=("$pkgname::git+https://github.com/Python-Markdown/markdown#tag=$pkgver")
sha256sums=('82f7a528ee08332aa154626585b13623de18ad3439986c18a902f77c5d1139f1')

prepare() {
  _patch_ "$pkgname"
}

build() {
  cd "$pkgname"
  python -m build --wheel --no-isolation
}

check() {
  cd "$pkgname"

  python -m unittest discover tests
}

package() {
  cd "$pkgname"

  python -m installer --destdir="$pkgdir" dist/*.whl

  # symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir/usr/share/licenses/$pkgname"
  ln -s "$site_packages/Markdown-$pkgver.dist-info/LICENSE.md" \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
