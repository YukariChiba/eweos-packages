# Maintainer: Aleksana QwQ <me@aleksana.moe>

pkgname=wlroots
pkgver=0.17.1
pkgrel=1
license=('MIT')
pkgdesc='Modular Wayland compositor library'
url='https://gitlab.freedesktop.org/wlroots/wlroots'
arch=(x86_64 aarch64 riscv64)
depends=('libdrm' 'libinput' 'seatd' 'libudev-zero' 'libxkbcommon' 'libgles' 'libegl' 'pixman' 'wayland' 'libdisplay-info')
makedepends=('flex' 'linux-headers' 'meson' 'wayland-protocols' 'hwdata')
provides=('libwlroots.so')
source=("$pkgname-$pkgver.tar.gz::$url/-/releases/$pkgver/downloads/wlroots-$pkgver.tar.gz")
sha256sums=('d58d68e3f90d92de4d49fa43b4d75dc78f8af1d920d090729331cefbdfcf361b')

build() {
    ewe-meson "$pkgname-$pkgver" build \
        -Ddefault_library=shared \
        -Dbackends=drm,libinput \
        -Drenderers=gles2 \
        -Dexamples=false \
        -Dxwayland=disabled \
        -Dxcb-errors=disabled
    ninja -C build
}

package() {
    DESTDIR="$pkgdir" ninja -C build install
    install -Dm644 "$pkgname-$pkgver/LICENSE" -t "$pkgdir/usr/share/licenses/$pkgname/"
}

