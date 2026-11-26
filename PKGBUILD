# Maintainer: Yukari Chiba <i@0x7f.cc>

_pkgname=u-msgpack-python
pkgname='python-u-msgpack'
pkgver=2.9.0
pkgrel=1
arch=('any')
url="https://github.com/vsergeev/${_pkgname}"
license=('MIT')
pkgdesc="portable, lightweight MessagePack serializer and deserializer for Python"
depends=('python')
makedepends=('python' 'python-setuptools' 'git')
checkdepends=('python-pytest')
source=("git+$url.git#tag=v$pkgver")
sha256sums=('3692c59c031adc4f86c57f764827bfcbaf44a95f16d8bde74465285e182bae28')

build() {
    cd "$_pkgname"
    python setup.py build
}

check() {
    cd "$_pkgname"
    pytest
}

package() {
    cd "$_pkgname"
    python setup.py install --root="${pkgdir}" --optimize=1 --skip-build

    install -Dm644 LICENSE "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
