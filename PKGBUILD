# Maintainer: Yao Zi <me@ziyao.cc>

pkgname=telegram-desktop
pkgver=7.4.6
pkgrel=1
pkgdesc='Official Telegram Desktop client'
url='https://desktop.telegram.org/'
arch=(x86_64 aarch64 loongarch64)
license=(GPL-3.0-or-later)
depends=(qt6-base qt6-svg qt6-imageformats qt6-wayland openh264 abseil-cpp
	 ffmpeg openssl libopus libvpx glib glibmm libdispatch hunspell
	 kcoreaddons openal-soft rnnoise xxhash zlib-ng boost-libs tl-expected
	 libavif libheif libjxl protobuf libsrtp libpipewire ada-url minizip-ng
	 pango hicolor-icon-theme)
makedepends=(cmake ninja boost libtg_owt gobject-introspection lld git gperf rust
	     qt6-base-devel qt6-shadertools)
_apiid=611335
_apihash=d524b414d21f4d37f08684c1df41ac9c
# Committed on 2026.11.23
_tdlib_commit=1b9efe84d6e9a2e2f6eadeeea32b0726d2b8c25d
_tlottie_ver=1.0.6
_wallet_engine_commit=e59e0d89d7ee90c388bf36e3334c5b276f396697
_patches_commit=8a28b8433af70771c3d101c776ad837a94bd47ec
# 0001: Downstream, LLD has a lower peak memory requirement than Mold.
# 0002: Downstream, link the Rust static library against libunwind.
# 0003: Downstream, define __X32_SYSCALL_BIT for musl on x86_64.
# wallet-engine.diff: Downstream, required by tdesktop 7.4.6.
# https://github.com/desktop-app/patches/blob/8a28b8433af70771c3d101c776ad837a94bd47ec/wallet-engine.patch
source=("https://github.com/telegramdesktop/tdesktop/releases/download/v$pkgver/tdesktop-$pkgver-full.tar.gz"
	"git+https://github.com/tdlib/td.git#commit=$_tdlib_commit"
	"tlottie-$_tlottie_ver.tar.gz::https://github.com/dkaraush/tlottie/archive/refs/tags/v$_tlottie_ver.tar.gz"
	"wallet-engine-$_wallet_engine_commit.tar.gz::https://github.com/i582/wallet-engine/archive/$_wallet_engine_commit.tar.gz"
	"wallet-engine.diff::https://github.com/desktop-app/patches/raw/$_patches_commit/wallet-engine.patch"
	"0001-use-lld.patch"
	"0002-link-libunwind.patch"
	"0003-define-x32-syscall-bit.patch"
	"tdesktop_rust.Cargo.toml"
	"tdesktop_rust.Cargo.lock"
	"tdesktop_rust.lib.rs")
sha256sums=('259afdd1a3a99c1f5155f856e92c55eff038d2639fba19fcfd91b27664a82370'
            'b0c3fadc449d45360559efb531736f2e2b1daa9d89af5d2425797019eff0fd0c'
            'a85dd1a8f62ca85248af380d5eee6f32e84b29c45134615b23355207ccb90359'
            '45d22ed481dc4fab07390abfa811c095c424e11c745e87b9d0d27b40efa17da2'
            '47dcde3477e056de86ba13c8cf55eadf4b1309d0e904bbe06ab0592f0fbe2cfe'
            'e80a974439d7384dd05c4befb1a39e081a154476dbfd707d3bab3712d826d5a1'
            'a52b6e3a2da9084f60c20e0a9bcde9a8623105b4a307552b827d962f789f43df'
            '7f6b7914b42592cb12b804eb1a8b3e73acc9ffe6c76bd194573a1f837c32ab57'
            '996ec9ca8536b9a6d188b4a9a1175af126652f6660e9d33e9f8ab7824e8b940a'
            '0545bfd8057ebd2448b1fa12b32e1e5ac6bba487ccaab57135b2780012eb4a3d'
            '87d9e03fd981f05b9c3c0d92a7b712f3584e3f6a9ad03eae11e2ac916310784b')

prepare() {
	_patch_ "tdesktop-$pkgver-full"

	patch -Np1 -d "wallet-engine-$_wallet_engine_commit" < wallet-engine.diff

	install -d "$srcdir/tdesktop_rust/src"
	install -m644 tdesktop_rust.Cargo.toml "$srcdir/tdesktop_rust/Cargo.toml"
	install -m644 tdesktop_rust.Cargo.lock "$srcdir/tdesktop_rust/Cargo.lock"
	install -m644 tdesktop_rust.lib.rs "$srcdir/tdesktop_rust/src/lib.rs"

	CARGO_HOME="$srcdir/build/widget_helper_rust/cargo" \
		cargo fetch --locked \
		--manifest-path "tdesktop-$pkgver-full/Telegram/ThirdParty/twidget/rust/Cargo.toml"
	CARGO_HOME="$srcdir/cargo" \
		cargo fetch --locked \
		--manifest-path "$srcdir/tdesktop_rust/Cargo.toml"
	CARGO_HOME="$srcdir/cargo" \
		cargo fetch --locked \
		--manifest-path "$srcdir/wallet-engine-$_wallet_engine_commit/bindgen/cpp/bindgen/Cargo.toml"
}

build () {
	export MAKEFLAGS="-j$jobs CC=cc CXX=c++"
	export LDFLAGS="$LDFLAGS -Wl,-z,stack-size=$((1024 * 1024)) -fuse-ld=lld"
	export CARGO_NET_OFFLINE=true

	# tlottie and wallet-engine are built as one Rust static library to avoid
	# duplicate standard library symbols.
	cd "$srcdir/tdesktop_rust"
	CARGO_HOME="$srcdir/cargo" cargo rustc \
		--lib --release --locked \
		--crate-type staticlib --crate-type cdylib \
		--config "profile.release.opt-level='z'" \
		--config "profile.release.lto='thin'" \
		--config "profile.release.codegen-units=1" \
		--config "profile.release.panic='unwind'" \
		--config "profile.release.package.tlottie.opt-level=3"
	install -d "$srcdir/tdesktop_rust-install/lib" \
		"$srcdir/tdesktop_rust-install/include/tlottie" \
		"$srcdir/tdesktop_rust-install/include/wallet_engine"
	CARGO_HOME="$srcdir/cargo" cargo run --locked \
		--manifest-path "$srcdir/wallet-engine-$_wallet_engine_commit/bindgen/cpp/bindgen/Cargo.toml" \
		-- --library \
		--out-dir "$srcdir/tdesktop_rust-install/include/wallet_engine" \
		target/release/libtdesktop_rust.so
	install -Dm644 target/release/libtdesktop_rust.a \
		"$srcdir/tdesktop_rust-install/lib/libtdesktop_rust.a"
	install -Dm644 "$srcdir/tlottie-$_tlottie_ver/include/tlottie.h" \
		"$srcdir/tdesktop_rust-install/include/tlottie/tlottie.h"
	cd "$srcdir"

	# Telegram requires the TDE2E part of tdlib. As it's not used by any
	# other packages, let's build it in place.
	cmake -B build-tde2e td -G Ninja \
		-DCMAKE_INSTALL_PREFIX="$srcdir/tde2e-install"	\
		-DCMAKE_BUILD_TYPE=Release			\
		-DTD_E2E_ONLY=ON
	cmake --build build-tde2e
	cmake --install build-tde2e

	CMAKE_PREFIX_PATH="$srcdir/tde2e-install:$srcdir/tdesktop_rust-install" \
	cmake -B build "tdesktop-$pkgver-full" -G Ninja \
		-DCMAKE_INSTALL_PREFIX=/usr			\
		-DCMAKE_INSTALL_LIBEXECDIR=lib		\
		-DCMAKE_BUILD_TYPE=Release			\
		-DDESKTOP_APP_USE_PACKAGED=ON			\
		-DDESKTOP_APP_DISABLE_X11_INTEGRATION=ON	\
		-DTDESKTOP_API_ID=$_apiid			\
		-DTDESKTOP_API_HASH=$_apihash
	cmake --build build
}

check() {
	ctest --test-dir build
}

package() {
	DESTDIR="$pkgdir" cmake --install build
}
