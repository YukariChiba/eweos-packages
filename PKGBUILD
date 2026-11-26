# Maintainer: Yukari Chiba <i@0x7f.cc>

_name=urllib3
pkgname=python-urllib3
pkgver=2.8.0
pkgrel=1
pkgdesc="HTTP library with thread-safe connection pooling and file post support"
arch=("any")
url="https://github.com/urllib3/urllib3"
license=("MIT")
depends=('python')
makedepends=(
  'python-build'
  'python-hatch-vcs'
  'python-hatchling'
  'python-installer'
  'python-wheel'
)
source=("https://github.com/urllib3/urllib3/archive/$pkgver/$pkgname-$pkgver.tar.gz")
sha512sums=('cc263e675c3409a4d474b1f618669435479ea819824d1971b8583892dbf27cf2ee4ba21acf23a1762134c6e7fd35a99697e063e4625a86e0879da4cb643739cc')


build() {
  cd $_name-$pkgver
  export SETUPTOOLS_SCM_PRETEND_VERSION=$pkgver
  python -m build --wheel --no-isolation --skip-dependency-check
}

# FIXME: missing check dependencies

package() {
  cd $_name-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE.txt -t "$pkgdir"/usr/share/licenses/$pkgname/
}
