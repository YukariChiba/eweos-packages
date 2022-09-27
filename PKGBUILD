# Maintainer: Felix Yan <felixonmars@gmail.com>

pkgname=perl-io-html
pkgver=1.004
pkgrel=3
pkgdesc="Open an HTML file with automatic charset detection"
arch=('any')
url='https://search.cpan.org/dist/IO-HTML'
depends=('perl')
license=('PerlArtistic' 'GPL')
options=('!emptydirs')
source=(https://search.cpan.org/CPAN/authors/id/C/CJ/CJM/IO-HTML-$pkgver.tar.gz)
sha512sums=('SKIP')

build() {
  export PERL_MM_USE_DEFAULT=1 PERL_MM_OPT="INSTALLDIRS=vendor" \
    PERL_MB_OPT="--installdirs vendor"
  cd IO-HTML-$pkgver
  perl Makefile.PL
  make 
}

check() {
  cd IO-HTML-$pkgver
  make test
}

package() {
  cd IO-HTML-$pkgver
  make DESTDIR="$pkgdir" install
}
