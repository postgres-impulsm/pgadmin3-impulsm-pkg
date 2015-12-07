# $Id$
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: Douglas Soares de Andrade <dsa@aur.archlinux.org>
# Contributor: Benjamin Andresen <benny@klapmuetz.org>
# Contributor: bekks <eduard.warkentin@gmx.de>

_orig_pkgname=pgadmin3
_orig_pkgver=1.20.0
_orig_pkgrel=5
pkgname=pgadmin3-impulsm
_gitpkgver=5d6f16c
pkgver=1.20.0.g$_gitpkgver
pkgrel=1
pkgdesc="Comprehensive design and management interface for PostgreSQL"
arch=('i686' 'x86_64')
url="http://www.pgadmin.org"
license=('custom')
depends=('wxgtk2.8' 'postgresql-libs' 'libxslt')
makedepends=('libpqxx' 'krb5' 'postgresql' 'imagemagick')
install=pgadmin3.install
source=("git+https://github.com/postgres-impulsm/pgadmin3.git#commit=$_gitpkgver"
        '0001-Move-misplaced-unlock-of-s_currentObjectMutex.patch')
md5sums=('SKIP'
         '69fbfdfe1bac75d7d1cdfeacd322cf5d')
conflicts=("$_orig_pkgname")
provides=("$_orig_pkgname=$_orig_pkgver")

prepare() {
  cd "$srcdir"
  convert pgadmin3/pgadmin/include/images/pgAdmin3.ico pgAdmin3.png

  cd "pgadmin3"
  ./bootstrap
  sed -i 's/wx-config/wx-config-2.8/' configure
  sed -i 's/wxrc/wxrc-2.8/g' stringextract pgadmin/ui/embed-xrc

  patch -p1 <$srcdir/0001-Move-misplaced-unlock-of-s_currentObjectMutex.patch
}

build() {
  cd "$srcdir"/pgadmin3
  [ -f Makefile ] ||  ./configure --prefix=/usr --with-wx-version=2.8
  make
}

package() {
  cd "$srcdir"/pgadmin3

  make DESTDIR="$pkgdir/" install
  install -Dm644 i18n/pgadmin3.lng "$pkgdir/usr/share/pgadmin3/i18n"
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/pgadmin3/LICENSE"

  install -Dm644 pgadmin/include/images/pgAdmin3.ico "$pkgdir/usr/share/pgadmin3/pgAdmin3.ico"
  install -Dm644 "$srcdir/pgAdmin3-0.png" "$pkgdir/usr/share/pgadmin3/pgAdmin3.png"

  install -Dm644 "$srcdir/pgAdmin3-3.png" "$pkgdir/usr/share/icons/hicolor/16x16/apps/pgAdmin3.png"
  install -Dm644 "$srcdir/pgAdmin3-2.png" "$pkgdir/usr/share/icons/hicolor/32x32/apps/pgAdmin3.png"
  install -Dm644 "$srcdir/pgAdmin3-1.png" "$pkgdir/usr/share/icons/hicolor/48x48/apps/pgAdmin3.png"

  install -Dm644 "pkg/pgadmin3.desktop" "$pkgdir/usr/share/applications/pgadmin3.desktop"
}
