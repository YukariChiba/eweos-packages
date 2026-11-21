# Maintainer: Yao Zi <ziyao@disroot.org>

pkgname=tftp-hpa
pkgver=7.2
pkgrel=1
pkgdesc='TFTP server ported to Linux'
url='https://git.kernel.org/pub/scm/network/tftp/tftp-hpa.git'
arch=(x86_64 aarch64 riscv64 loongarch64)
license=(BSD-3-Clause BSD-4-Clause-UC)
depends=(musl readline libcap)
makedepends=(linux-uapi-headers)
backup=(etc/conf.d/tftpd.conf)
source=("https://www.kernel.org/pub/software/network/tftp/$pkgname-$pkgver.tar.xz"
	"tftpd.service"
	"tftpd.tmpfiles"
	"tftpd.conf")
sha256sums=('72858bb18cff6207ffc98fe8d21e6a1187e036163ca8d91e9c9f5d4c3fdae22f'
            '3ca9451f963f3f570ac0e63a8f9bb3e927d4df063779b39a31a4c06f7b163d23'
            '7d252c4680f8929807a18aac57db4ab45c8fb6ce5f8a733b5dc1ad3600fec26b'
            'c84efa2fc0b3f86cf7b00e2d1740432a37b6c8c6e7800e28bcfea2a05a471492')

build() {
	cd "$pkgname-$pkgver"

	./configure --prefix=/usr \
		--sbindir=/usr/bin
	make
}

check() {
	cd "$pkgname-$pkgver"

	# tests/test-tftp.sh requires --jail, which needs openat2(); musl does not
	# expose openat2(). Exercise one download and one upload with --secure
	# instead, matching the service's chroot mode.
	(
		set -e
		root=$(mktemp -d)
		out=$(mktemp -d)
		pid=
		trap 'test -n "$pid" && kill "$pid" 2>/dev/null || true; rm -rf "$root" "$out"' EXIT

		mkdir -p "$root/files" "$root/upload"
		printf 'tftp-hpa test\n' > "$root/files/test.txt"
		chmod 755 "$root"
		chmod 777 "$root/upload"

		./tftpd/tftpd --stderr -L -p --port-range 60969:60999 \
			-a 127.0.0.1:16971 -c -s "$root" >"$out/server.log" 2>&1 &
		pid=$!
		sleep 1
		kill -0 "$pid"

		./tftp/tftp -B 512 -W 1 -m octet 127.0.0.1 16971 \
			-c get files/test.txt "$out/test.txt"
		cmp "$root/files/test.txt" "$out/test.txt"

		./tftp/tftp -B 512 -W 1 -m octet 127.0.0.1 16971 \
			-c put "$root/files/test.txt" upload/test.txt
		cmp "$root/files/test.txt" "$root/upload/test.txt"
	)
}

package() {
	cd "$pkgname-$pkgver"

	make install INSTALLROOT="$pkgdir"

	_dinit_install_services_ "$srcdir"/tftpd.service
	install -Dm644 "$srcdir"/tftpd.tmpfiles \
		"$pkgdir"/usr/lib/tmpfiles.d/tftpd.conf
	install -Dm644 "$srcdir"/tftpd.conf "$pkgdir"/etc/conf.d/tftpd.conf
	_install_license_ "$srcdir/$pkgname-$pkgver/LICENSES/BSD-3-Clause.txt" BSD-3-Clause.txt
	_install_license_ "$srcdir/$pkgname-$pkgver/LICENSES/BSD-4-Clause-UC.txt" BSD-4-Clause-UC.txt
}
