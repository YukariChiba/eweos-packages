# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-soupsieve
pkgver=4.1.3
pkgrel=1
pkgdesc='A CSS4 selector implementation for Beautiful Soup'
arch=('any')
url='https://github.com/facelessuser/soupsieve'
license=('MIT')
depends=('python')
makedepends=(
  'git'
  'python-build'
  'python-installer'
  'python-hatchling'
)
checkdepends=(
  'python-pytest'
  'python-beautifulsoup4'
  'python-html5lib'
  'python-lxml'
)
source=("$pkgname::git+$url#tag=$pkgver")
sha256sums=('0a5a5e274d3cda50dbe84df3a88019f68f4fda7cdb45ec994bad755452d1f4af')

build() {
  cd "$pkgname"
  python -m build --wheel --no-isolation
}

check() {
  cd "$pkgname"
  pytest
}

package() {
  cd "$pkgname"

  python -m installer --destdir="$pkgdir" dist/*.whl

  # symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "$pkgdir/usr/share/licenses/$pkgname"
  ln -s "$site_packages/${pkgname#python-}-$pkgver.dist-info/licenses/LICENSE.md" \
    "$pkgdir/usr/share/licenses/$pkgname/LICENSE.md"
}
