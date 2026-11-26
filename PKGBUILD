# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-iniconfig
pkgver=2.3.1
pkgrel=1
pkgdesc="brain-dead simple config-ini parsing"
url="https://github.com/pytest-dev/iniconfig"
license=('MIT')
arch=('any')
depends=('python')
makedepends=('git' 'python-build' 'python-installer' 'python-hatchling' 'python-hatch-vcs')
checkdepends=('python-pytest')
source=("git+$url.git#tag=v$pkgver")
sha512sums=('8283345318f5e1bcc159dca6a33f7d0c90164a7604d7ee9cc56973d078b741b90f9436b23d267be19b691ca3b90c45f192d806161a4d22a5320fdf6465acf9fe')

build() {
  cd iniconfig
  python -m build -nw
}

check() {
  cd iniconfig
  PYTHONPATH="$PWD/src" pytest
}

package() {
  cd iniconfig
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname/
}
