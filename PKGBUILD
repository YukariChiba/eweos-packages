# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-pyparsing
pkgver=3.3.3
pkgrel=1
pkgdesc='General parsing module for Python'
arch=('any')
url='https://github.com/pyparsing/pyparsing/'
license=('MIT')
depends=('python')
makedepends=('python-build' 'python-installer' 'python-flit-core')
optdepends=('python-railroad-diagrams: for generating Railroad Diagrams'
            'python-jinja: for generating Railroad Diagrams')
source=("https://github.com/pyparsing/pyparsing/archive/$pkgver/$pkgname-$pkgver.tar.gz")
sha512sums=('286bc52c3914ca874d3aab32db3505fc152b1511f1779a49fc00958a3d7ab6320d777857a8df4e4f55bfdc177e55779548e909722fe52ab1660eca02785f57fd')

build() {
  cd pyparsing-$pkgver
  python -m build -nw
}

package() {
  cd pyparsing-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -Dm644 LICENSE -t "$pkgdir"/usr/share/licenses/$pkgname/
}
