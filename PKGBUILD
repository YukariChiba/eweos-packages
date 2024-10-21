# Maintainer:
# Contributor: George Rawlinson <grawlinson@archlinux.org>

pkgbase=openldap
pkgname=('libldap')
pkgver=2.6.3
pkgrel=2
arch=(x86_64 aarch64 riscv64 loongarch64)
url="https://www.openldap.org/"
license=('custom')
makedepends=('cyrus-sasl' 'e2fsprogs' 'util-linux-libs' 'chrpath' 'unixodbc' 'libsodium' 'libltdl' 'mandoc-soelim' 'libxcrypt')
options=('!makeflags' 'emptydirs')
source=(
  https://www.openldap.org/software/download/OpenLDAP/openldap-release/${pkgbase}-${pkgver}.tgz
  openldap.tmpfiles
  openldap.sysusers
  Add-UNIX_LINK_LIBS-Makefile.patch
  remove_la_references.patch)
sha256sums=('d2a2a1d71df3d77396b1c16ad7502e674df446e06072b0e5a4e941c3d06c0d46'
            '0be46138e53ff2fa6d4b4c06bfbdd2100426e0bd2ed29bf3419ade6b5974e9a0'
            'bb6a9af3b5cce594b2e737b641d2edfa327fde63c85a26c824fd2246e0839de5'
            'ce8e66ac525c4261c998c1041f8cb126933eb767fcc8b7e61c6e7707e7d17420'
            '3fe777e3f38a602e5b5ca3cb5b68b4fb6c6346c7bdaf7f9c08a9b70a61c0d211')
options=(!lto)

# extra modules found in contrib/slapd-modules
_extra_modules=(
  'nssov'
  'autogroup'
  'lastbind'
  'passwd/sha2'
)

prepare()
{
  cd ${pkgbase}-${pkgver}

  patch -p1 < $srcdir/Add-UNIX_LINK_LIBS-Makefile.patch
  patch -p1 < $srcdir/remove_la_references.patch
  # change perms from 0644 to 0755
  sed -i 's|-m 644 $(LIBRARY)|-m 755 $(LIBRARY)|' libraries/{liblber,libldap}/Makefile.in

  # change rundir to /run/openldap
  sed -i 's|#define LDAPI_SOCK LDAP_RUNDIR LDAP_DIRSEP "run" LDAP_DIRSEP "ldapi"|#define LDAPI_SOCK LDAP_DIRSEP "run" LDAP_DIRSEP "openldap" LDAP_DIRSEP "ldapi"|' include/ldap_defaults.h
  sed -i 's|%LOCALSTATEDIR%/run|/run/openldap|' servers/slapd/slapd.{conf,ldif}
  sed -i 's|-$(MKDIR) $(DESTDIR)$(localstatedir)/run|-$(MKDIR) $(DESTDIR)/run/openldap|' servers/slapd/Makefile.in

  # modify upstream systemd service
  sed -i -e "s|EnvironmentFile.*|EnvironmentFile=-/etc/conf.d/slapd|" -e "s/slapd -d 0/\0 -u ldap -g ldap/" servers/slapd/slapd.service

  autoreconf -fvi
  # WARNING! Skipping posix regex check!
  sed -i "s/ol_cv_c_posix_regex=no/ol_cv_c_posix_regex=yes/g" configure
}

build()
{
  cd ${pkgbase}-${pkgver}
  ./configure \
    --prefix=/usr \
    --libexecdir=/usr/lib \
    --sysconfdir=/etc \
    --localstatedir=/var/lib/openldap \
    --sbindir=/usr/bin \
    --enable-dynamic \
    --enable-syslog \
    --enable-ipv6 \
    --enable-local \
    --enable-crypt \
    --enable-spasswd \
    --enable-modules \
    --enable-backends \
    --enable-argon2 \
    --with-argon2=libsodium \
    --disable-wt \
    --enable-overlays=mod \
    --with-cyrus-sasl \
    --with-systemd=no \
    --with-threads

  sed -i -e 's/ -shared / -Wl,-O1,--as-needed\0/g' libtool

  make

  # build extra modules
  for module in "${_extra_modules[@]}"; do
    make -C "contrib/slapd-modules/$module" \
      OPT="$CFLAGS $CPPFLAGS" \
      prefix=/usr \
      libexecdir=/usr/lib \
      sysconfdir=/etc/openldap
  done
}

check()
{
  cd ${pkgbase}-${pkgver}
  #make test
}

package_libldap()
{
  pkgdesc="Lightweight Directory Access Protocol (LDAP) client libraries"
  depends=('e2fsprogs' 'libxcrypt') # add libsasl later!
  backup=('etc/openldap/ldap.conf')

  cd ${pkgbase}-${pkgver}
  for dir in include libraries doc/man/man3; do
    pushd ${dir}
    make DESTDIR="${pkgdir}" install
    popd
  done
  install -Dm644 -t "$pkgdir/usr/share/man/man5" doc/man/man5/ldap.conf.5

  # remove duplicate conf files
  rm "${pkgdir}"/etc/openldap/*.default

  # shared library versioning
  ln -sf liblber.so "${pkgdir}"/usr/lib/liblber.so.2
  ln -sf libldap.so "${pkgdir}"/usr/lib/libldap.so.2

  # license
  install -Dm644 -t "${pkgdir}/usr/share/licenses/${pkgname}" LICENSE
}
