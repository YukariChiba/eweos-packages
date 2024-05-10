# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=glib
pkgver=2.80.1
_pkgver_major=${pkgver%.*}
pkgrel=2
pkgdesc="Low-level core library that forms the basis for projects such as GTK+ and GNOME"
url="https://wiki.gnome.org/Projects/GLib"
license=(LGPL)
arch=(x86_64 aarch64 riscv64)
depends=(pcre2 libffi util-linux-libs zlib)
makedepends=(gettext python libelf util-linux meson dbus python-packaging gobject-introspection)
provides=(glib2)
source=(
  "https://download.gnome.org/sources/$pkgname/${_pkgver_major}/$pkgname-$pkgver.tar.xz"
  glib-compile-schemas.hook
  ld-test.patch
)
sha256sums=('bcfc8c2fab64fc9dcb91011375422159f1440502257fb90219215079d8716705'
            'e42404979cc47959a3e560bf6f6c52b9fc90e1566ebb9b5cafb29d7f4cb4fe5f'
            '7dbc500d47f9059137cd2fcf1e3df8b9f33397cb7f0b7a9aba74d60940109b66')

prepare()
{
  _patch_ $pkgname-$pkgver
}

build()
{
  ewe-meson $pkgname-$pkgver build \
    --default-library both \
    -D glib_debug=disabled \
    -D selinux=disabled \
    -D sysprof=disabled \
    -D libmount=disabled \
    -D gtk_doc=false \
    -D man-pages=disabled
  meson compile -C build
}

check() {
  meson test --timeout-multiplier 2 --no-rebuild --print-errorlogs -C build
}

package()
{
  meson install -C build --destdir "$pkgdir"
  install -Dt "$pkgdir/usr/share/libalpm/hooks" -m644 *.hook
}
