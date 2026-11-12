# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=wf-shell
pkgver=0.11.0
pkgrel=1
pkgdesc='GTK4-based panel for the Wayfire compositor'
url=https://wayfire.org
arch=(x86_64 aarch64 riscv64 loongarch64)
license=(MIT)
depends=(alsa-lib gtk4-layer-shell gtkmm hicolor-icon-theme libdbusmenu-glib libdrm libepoxy libpulse libwireplumber libxkbcommon mesa openssl pam wf-config yyjson)
makedepends=(wayland wayfire wayland-protocols meson ninja git gobject-introspection glib2 glm libpipewire wlroots0.20-devel)
backup=(etc/pam.d/wf-locker etc/xdg/xdg-desktop-portal-wlr/wayfire)

# Submodules are pinned to the commits recorded by the v$pkgver tag.
#
# 0001: Downstream, clang cannot use WfOption<T>'s deduced conversion operator
# inherited from a template base in a switch statement.
# TODO: upstream it.
source=(
  "${pkgname}::git+https://github.com/WayfireWM/wf-shell#tag=v$pkgver"
  git+https://gitlab.gnome.org/GNOME/libgnome-volume-control.git#commit=5f9768a2eac29c1ed56f1fbb449a77a3523683b6
  git+https://github.com/soreau/wayland-logout.git#commit=1cffc6fd0be5d8127f394b25eb3c82e71fbaabe1
  git+https://github.com/WayfireWM/wf-json.git#commit=70039e13cdeaebd8ec498ed30bf5ab91c2e313ec
  "0001-locker-use-explicit-option-value-in-switch.patch"
)
sha512sums=('d8c19cc4828361c931cbcec529de539f00f8d248b13d64d10b3e2debddd4587a8bf6ad5ee388b630f4e512a5ad98638bb9df0fb9d96f75d81d28584935f237d4'
            '5bb7e89208aa97c67754b82b071e945d3aacc161c6a1dae16b41cc294bb6f28c3c5cfd4e79f8a8e62454bb466b8ed30856d5189dd320e1fe89a920197ad398a0'
            '8f10e9b46e66b1e06792869f48197ad43e75b90d75d6c74e49931ad4fd75894c2719c429ea0d22db41353d100fc441b276a9f980518379345d45cff07df2281f'
            'b2cb5c0c4cb4e03e1863fe954ef7661453cf5d872c2b6a39c45a47034a53eb4cb9211517296663c8a483072d6e89550d0e5808c973ca72a5ce9d2211dccb1eaa'
            'da68868bae632430a575bd814594daf19b3e5e8136bfaf9e36c24779a1c80c5c574d4a9832f5805d314b7dd07db508888c92dbfa5b5cd19bd7bd9d218e875834')

prepare() {
  cd "$pkgname"
  _patch_ "$pkgname"

  git submodule init
  # gtk4-layer-shell is provided by the eweOS package.
  git config submodule.subprojects/gtk4-layer-shell.update none
  git submodule set-url subprojects/gvc "$srcdir/libgnome-volume-control"
  git submodule set-url subprojects/wayland-logout "$srcdir/wayland-logout"
  git submodule set-url subprojects/wf-json "$srcdir/wf-json"
  git -c protocol.file.allow=always submodule update
}

build() {
  # ddcutil is not packaged in eweOS.
  ewe-meson "$pkgname" build -Dddcutil=disabled
  meson compile -C build
}

check() {
  meson test -C build --print-errorlogs
}

package() {
  meson install -C build --destdir "$pkgdir"
  cd "$pkgname"
  _install_license_ "$srcdir/$pkgname/LICENSE" LICENSE
  install -Dm644 wf-shell.ini.example "$pkgdir/usr/share/doc/$pkgname/wf-shell.ini.example"
}
