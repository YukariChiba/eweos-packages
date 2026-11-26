# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=python-typing_extensions
_name=${pkgname#python-}
pkgver=4.16.0
pkgrel=1
pkgdesc='Backported and Experimental Type Hints for Python 3.8+'
arch=(any)
url=https://github.com/python/typing_extensions
license=(Python-2.0.1)
depends=(python)
makedepends=(git python-build python-flit-core python-installer)
checkdepends=(python-tests python-typing_extensions)
provides=(python-typing-extensions)
conflicts=(python-typing-extensions)
# 0001: Downstream, skip a test invalidated by CPython 3.13 literal deduplication
source=("git+${url}.git#tag=${pkgver}"
        "0001-skip-test-args.patch")
sha256sums=('3fd066549a36de50bf51524a6df9ca44c2e3557ced750c5a46dc5d4cb83fc726'
            'bf5d4df2581b77693655761d718bbdc1c431c76313675eac917bf612e16bc99a')

prepare() {
  _patch_ "$_name"
}

build() {
  cd "${_name}"
  python -m build --wheel --skip-dependency-check --no-isolation
}

check() {
  cd "${_name}"
  python -m unittest discover src
}

package() {
  cd "${_name}"
  python -m installer --destdir="${pkgdir}" dist/*.whl

  # Symlink license file
  local site_packages=$(python -c "import site; print(site.getsitepackages()[0])")
  install -d "${pkgdir}"/usr/share/licenses/${pkgname}
  ln -s "${site_packages}"/"${_name}"-${pkgver}.dist-info/LICENSE \
    "${pkgdir}"/usr/share/licenses/${pkgname}/LICENSE
}
