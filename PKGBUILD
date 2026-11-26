# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-filelock
pkgver=4.0.10
pkgrel=1
pkgdesc="A platform independent file lock"
url="https://github.com/benediktschmitt/py-filelock"
license=('custom:Unlicense')
arch=('any')
depends=('python')
makedepends=('git' 'python-build' 'python-installer' 'python-hatchling' 'python-hatch-vcs')
#checkdepends=(
#  'python-pytest'
#  'python-pytest-timeout'
#  'python-pytest-mock'
#  'python-pytest-asyncio'
#  'python-virtualenv'
#)
source=("git+https://github.com/benediktschmitt/py-filelock.git#tag=$pkgver")
sha512sums=('e9abd998f6d9e98c488631e33bda57906dd7f21d62b7834111229c5742851081c82902b5ed8f3a54fea34cf98ad804c49f0d676c12db306545b417f95a7ba999')

build() {
  cd py-filelock
  python -m build --wheel --no-isolation
}

#FIXME: missing python-virtualenv
#check() {
#  cd py-filelock
#  PYTHONPATH=src pytest tests
#}

package() {
  cd py-filelock
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname/
}
