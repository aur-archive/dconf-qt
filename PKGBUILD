# Maintainer: György Balló <ballogy@freestart.hu>
pkgname=dconf-qt
pkgver=0.0.0.110722
pkgrel=3
pkgdesc="Qt and QML bindings for dconf"
arch=('i686' 'x86_64')
url="https://launchpad.net/dconf-qt"
license=('LGPL')
depends=('qt' 'dconf')
makedepends=('cmake')
source=(https://launchpad.net/ubuntu/+archive/primary/+files/${pkgname}_$pkgver.orig.tar.bz2
        01_fix_pc_generation.patch
        02_link_again_dconf_dbus.patch)
md5sums=('39b34290852194f7017ed95fc368ad0f'
         'b4595c245807b3387b715a0e47099e42'
         'cfca46143b82fc23fe4cb570b0e9fa28')

build() {
  cd "$srcdir/lib$pkgname-0.0.0"
  patch -Np1 -i "$srcdir/01_fix_pc_generation.patch"
  patch -Np1 -i "$srcdir/02_link_again_dconf_dbus.patch"

  # Fix imports directory
  sed -i 's|lib/qt4/imports|${QT_IMPORTS_DIR}|' qml/CMakeLists.txt

  cmake . -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release
  make
}

package() {
  cd "$srcdir/lib$pkgname-0.0.0"

  make DESTDIR="$pkgdir/" install
}
