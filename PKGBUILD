# Maintainer: Yukari Chiba <i@0x7f.cc>

pkgname=polkit-gnome
pkgver=0.105
pkgrel=1
pkgdesc='Legacy polkit authentication agent for GNOME'
arch=(x86_64 aarch64 riscv64)
url='https://gitlab.gnome.org/Archive/policykit-gnome'
license=('LGPL')
depends=('gtk3' 'polkit')
makedepends=('intltool')
source=("https://download.gnome.org/sources/$pkgname/$pkgver/$pkgname-$pkgver.tar.xz"
        'polkit-gnome-authentication-agent-1.desktop'
        '0001-Select-the-current-user-to-authenticate-with-by-defa.patch'
        '0002-Auth-dialog-Make-the-label-wrap-at-70-chars.patch'
	'0003-Get-user-icon-from-accountsservice-instead-of-lookin.patch')
sha256sums=('1784494963b8bf9a00eedc6cd3a2868fb123b8a5e516e66c5eda48df17ab9369'
            '5074c723a4eab274830587d799ba781ff57f4fbe4ac99fbdc5aac5009c441ee7'
            'b989f1c7e30f2f9f9ef03f1a06db708d83c4945ee242ca573e7d66b64bf7037f'
            '41afbd11bdf4633dc619675862078c23e4b200c888da1569d030c502999b25d8'
            '4ee38d2dae6e592040c41ba07caa284135dc232feef5a30acb42c0e28340adce')

prepare() {
  _patch_ $pkgname-$pkgver
}

build() {
  cd $pkgname-$pkgver
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var --libexecdir=/usr/lib/$pkgname
  make
}

package() {
  cd $pkgname-$pkgver
  make DESTDIR="$pkgdir" install
  install -Dm644 "$srcdir/polkit-gnome-authentication-agent-1.desktop" \
      "$pkgdir/usr/share/applications/polkit-gnome-authentication-agent-1.desktop"
}
