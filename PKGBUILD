# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-pytest-benchmark
pkgver=5.3.1
pkgrel=1
pkgdesc='A py.test fixture for benchmarking code'
arch=('any')
license=('BSD-2-Clause')
url='https://github.com/ionelmc/pytest-benchmark'
depends=('python-pytest' 'python-py-cpuinfo')
makedepends=('python-setuptools' 'python-build' 'python-installer' 'python-wheel')
#checkdepends=('python-pygal' 'python-pygaljs' 'python-freezegun' 'mercurial' 'python-aspectlib'
#              'python-pytest-xdist' 'python-elasticsearch' 'git')
source=("$pkgname-$pkgver.tar.gz::https://github.com/ionelmc/pytest-benchmark/archive/v$pkgver.tar.gz")
sha512sums=('593cc0136a736ce331189d5720ab0b70de414d7614d3adcb53ed7d6772418d346bf08d28be7b9bf9bcb9af3ee6c6880c2d8ff69ed96aa9601c4673e72dfc9292')

prepare() {
  cd pytest-benchmark-$pkgver
}

build() {
  cd pytest-benchmark-$pkgver
  python -m build --wheel --no-isolation
}

check() {
  # Hack entry points by installing it
  # FIXME: missing dependencies
  cd pytest-benchmark-$pkgver
  #python setup.py install --root="$PWD/tmp_install" --optimize=1
  #local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  #PYTHONPATH="$PWD/tmp_install/$site_packages:$PYTHONPATH" PATH="$PWD/tmp_install/usr/bin:$PATH" python -m pytest tests
}

package() {
  cd "$srcdir"/pytest-benchmark-$pkgver
  python -m installer --destdir="$pkgdir" dist/*.whl
  install -D -m644 LICENSE "$pkgdir"/usr/share/licenses/$pkgname/LICENSE
}
