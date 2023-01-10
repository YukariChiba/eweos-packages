# Maintainer: Aleksana QwQ <me@aleksana.moe>
# Contributor: Giovanni Scafora <giovanni@archlinux.org>
# Contributor: Mark Rosenstand <mark@borkware.net>
# Contributor: Paul Mattal <paul@archlinux.org>

pkgname=perl-locale-gettext
_realname=Locale-gettext
pkgver=1.07
pkgrel=12
pkgdesc="Permits access from Perl to the gettext() family of functions"
arch=(x86_64 aarch64)
license=('GPL' 'PerlArtistic')
url="https://search.cpan.org/dist/${_realname}/"
depends=('gettext' 'perl' 'libxcrypt')
options=(!emptydirs)
source=("https://search.cpan.org/CPAN/authors/id/P/PV/PVANDRY/${_realname}-${pkgver}.tar.gz")
sha512sums=('SKIP')

build()
{
  cd "${srcdir}/${_realname}-${pkgver}"

  # install module in vendor directories.
  PERL_MM_USE_DEFAULT=1 perl Makefile.PL INSTALLDIRS=vendor
  make
}

check()
{
  cd "${srcdir}/${_realname}-${pkgver}"

  make test
}

package()
{
  cd "${srcdir}/${_realname}-${pkgver}"
  make install DESTDIR="${pkgdir}"

  # remove perllocal.pod and .packlist
  find "${pkgdir}" -name perllocal.pod -delete
  find "${pkgdir}" -name .packlist -delete
}
