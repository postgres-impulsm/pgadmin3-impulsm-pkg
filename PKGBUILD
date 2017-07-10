# $Id: PKGBUILD 225034 2017-04-24 12:16:13Z jgc $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: Douglas Soares de Andrade <dsa@aur.archlinux.org>
# Contributor: Benjamin Andresen <benny@klapmuetz.org>
# Contributor: bekks <eduard.warkentin@gmx.de>

pkgname=pgadmin3-impulsm
_gitpkgver=02f8582
pkgver=1.22.2+git$_gitpkgver
pkgrel=1
conflicts=("pgadmin3")
provides=("pgadmin3=1.22.2")
pkgdesc="Comprehensive design and management interface for PostgreSQL"
arch=('i686' 'x86_64')
url="http://www.pgadmin.org"
license=('custom')
depends=('wxgtk' 'postgresql-libs' 'libxslt' 'libgcrypt')
makedepends=('libpqxx' 'krb5' 'postgresql' 'imagemagick')
validpgpkeys=('E0C4CEEB826B1FDA4FB468E024ADFAAF698F1519')
source=("git+https://github.com/postgres-impulsm/pgadmin3.git#commit=$_gitpkgver"
        pgadmin3-fix-segfault.patch)
sha256sums=('SKIP'
            'b175869b77bcbfa43f1bc256277966882789883792c4f9dd26038ec248def6a2')

prepare() {
  cd "$srcdir"
  #ORIG_PKG_LINE#convert pgadmin3-${pkgver}/pgadmin/include/images/pgAdmin3.ico pgAdmin3.png
  convert pgadmin3/pgadmin/include/images/pgAdmin3.ico pgAdmin3.png

# Fix segfault at startup (Debian)
  #ORIG_PKG_LINE#cd $pkgname-$pkgver
  cd pgadmin3

  patch -p1 -i ../pgadmin3-fix-segfault.patch
}

build() {
  #ORIG_PKG_LINE#cd "$srcdir"/pgadmin3-${pkgver}
  cd "$srcdir/pgadmin3"

  ./bootstrap
  ./configure --prefix=/usr --with-wx-version=3.0 --with-libgcrypt
  make
}

package() {
  #ORIG_PKG_LINE#cd "$srcdir"/pgadmin3-${pkgver}
  cd "$srcdir/pgadmin3"

  make DESTDIR="$pkgdir/" install
  #ORIG_PKG_LINE#install -Dm644 i18n/$pkgname.lng "$pkgdir/usr/share/pgadmin3/i18n"
  #ORIG_PKG_LINE#install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 i18n/pgadmin3.lng "$pkgdir/usr/share/pgadmin3/i18n"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/pgadmin3/LICENSE"

  install -Dm644 pgadmin/include/images/pgAdmin3.ico "$pkgdir/usr/share/pgadmin3/pgAdmin3.ico"
  install -Dm644 "$srcdir/pgAdmin3-1.png" "$pkgdir/usr/share/pgadmin3/pgAdmin3.png"

  install -Dm644 "$srcdir/pgAdmin3-3.png" "$pkgdir/usr/share/icons/hicolor/16x16/apps/pgAdmin3.png"
  install -Dm644 "$srcdir/pgAdmin3-2.png" "$pkgdir/usr/share/icons/hicolor/32x32/apps/pgAdmin3.png"
  install -Dm644 "$srcdir/pgAdmin3-1.png" "$pkgdir/usr/share/icons/hicolor/48x48/apps/pgAdmin3.png"

  install -Dm644 "pkg/pgadmin3.desktop" "$pkgdir/usr/share/applications/pgadmin3.desktop"
}
