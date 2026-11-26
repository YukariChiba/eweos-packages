# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-cattrs
_pipname=${pkgname#python-}
pkgver=26.2.1
pkgrel=1
pkgdesc='Complex custom class converters for attrs'
arch=(any)
#url='https://catt.rs'
url='https://github.com/python-attrs/cattrs'
license=(MIT)
depends=(python
         python-attrs)
makedepends=(git
	     python-build
             python-installer
             python-wheel
             python-hatch-vcs
             python-hatchling)
_archive="$_pipname"
source=("git+$url.git#tag=v$pkgver")
sha256sums=('1b71e643e636fab7a890b2c38ddeffa363b44e1cd20ca3df0d8601db5611dfd3')

build() {
	cd "$_archive"
	python -m build -wn
}

package() {
	cd "$_archive"
	python -m installer -d "$pkgdir" dist/*.whl
	install -Dm0644 -t "$pkgdir/usr/share/licenses/$pkgname/" LICENSE
}
