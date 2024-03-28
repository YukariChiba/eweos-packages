# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=polkit
pkgver=124
pkgrel=1
pkgdesc="Application development toolkit for controlling system-wide privileges"
url="https://gitlab.freedesktop.org/polkit/polkit"
arch=(x86_64 aarch64 riscv64)
license=(LGPL-2.0-or-later)
depends=(
  expat
  duktape
  glib
  pam
)
makedepends=(
  git
  gobject-introspection
  meson
  docbook-xsl
)
provides=(libpolkit-{agent,gobject}-1.so)
backup=(etc/pam.d/polkit-1)
source=(
  "git+https://gitlab.freedesktop.org/polkit/polkit.git#tag=$pkgver"
  0001-meson-Pass-polkitd_uid-to-meson_post_install.py.patch
  0001.patch
  0002.patch
  0003.patch
  polkit.sysusers
  polkitd.service
)
sha256sums=('SKIP'
            '3f38c437a792accd2ae22e46f41460d23ba7f1e389deef10b7015cccae15ab0d'
            'f6e878134c27ac89769c413dff804900f238874329fdd12e40bb797410b52157'
            '51bde7722db40f075ea87e5ee246e13ce8365a9728874b3f4cc754a8fb09ee6d'
            '58ffea6b0e7b6f28b50d445fcc3a773b28699876eba3695f240eb495db9c0a2a'
            '776e5e3954b732d855a39f6d51083a51981f171af27ea903ee9dabd9e6ffa4a0'
            '97928db56c3a60b354ba1d17141afda9a70defde7a628a94bee8a18642ddf95e')

prepare() {
  cd $pkgname
  patch -p1 < ../0001-meson-Pass-polkitd_uid-to-meson_post_install.py.patch
  mkdir -p subprojects/packagefiles
  cp $srcdir/000{1,2,3}.patch subprojects/packagefiles
  echo "diff_files = 0001.patch, 0002.patch, 0003.patch" >> subprojects/mocklibc.wrap
}

build() {
  CFLAGS+=" -D_GNU_SOURCE"

  local meson_options=(
    -D examples=true
    -D man=true
    -D os_type=redhat
    -D polkitd_uid=102
    -D polkitd_user=polkitd
    -D session_tracking=ConsoleKit
    -D tests=true
    -D gtk_doc=false
    -D authfw=pam
  )

  ewe-meson polkit build "${meson_options[@]}"
  meson compile -C build
}

check() {
  # FIXME: need python dbus
  meson test -C build --print-errorlogs -t 3 || :
}

package() {
  depends+=(dbus)
  meson install -C build --destdir "$pkgdir"

  mkdir -p $pkgdir/etc/pam.d
  mv $pkgdir/usr/lib/pam.d/polkit-1 $pkgdir/etc/pam.d/polkit-1
  rm -r $pkgdir/usr/lib/pam.d
  sed -i 's/system-auth/auth/' $pkgdir/etc/pam.d/polkit-1

  _install_sysusers_ $srcdir/polkit.sysusers
  _dinit_install_services_ $srcdir/polkitd.service
}
