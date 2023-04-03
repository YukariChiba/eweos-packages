# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Felix Yan <felixonmars@archlinux.org>
# Contributor: xRemaLx <anton.komolov@gmail.com>

pkgname=perl-extutils-installpaths
_pkgname=ExtUtils-InstallPaths
pkgver=0.012
pkgrel=6
pkgdesc="ExtUtils::InstallPaths - Build.PL install path logic made easy"
arch=('any')
license=('PerlArtistic' 'GPL')
url="https://search.cpan.org/dist/ExtUtils-InstallPaths/"
options=('!emptydirs')
depends=('perl' 'perl-extutils-config')
source=("https://search.cpan.org/CPAN/authors/id/L/LE/LEONT/${_pkgname}-${pkgver}.tar.gz")
sha512sums=('92a4e9ebb387d330ae67b0716b96b27165d08503d2915d8301b3a6aa185f962940e761d21fd400033e6a814e276918e0662da3740ca2852a53cf0fe54f3d7660')

build() {
  ( export PERL_MM_USE_DEFAULT=1 PERL5LIB=""                 \
      PERL_AUTOINSTALL=--skipdeps                            \
      PERL_MM_OPT="INSTALLDIRS=vendor DESTDIR='$pkgdir'"     \
      PERL_MB_OPT="--installdirs vendor --destdir '$pkgdir'" \
      MODULEBUILDRC=/dev/null

    cd "${srcdir}/${_pkgname}-${pkgver}"
    /usr/bin/perl Makefile.PL
    make
  )
}

check() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  ( export PERL_MM_USE_DEFAULT=1 PERL5LIB=""
    make test
  )
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  make install
  find "$pkgdir" -name .packlist -o -name perllocal.pod -delete
}
