# Mantainer: Jonas Heinrich <onny@project-insanity.org>
# Contributor: M0Rf30

pkgname=v-mobile-broadband
pkgver=3.00.01
pkgrel=5
pkgdesc="3G device manager for Linux"
arch=('i686' 'x86_64')
license=('GPL')
url="https://github.com/meh/vodafone-mobile-connect"
depends=('usb_modeswitch' 'python2-pytz' 'python2-pysqlite' 'ozerocdoff' 'dbus-python' 'twisted' 'python2-pyserial' 'wvdial' 'python2-pyasn1' 'python2-notify' 'gnome-python-extras' 'pygtk' 'pyxml' 'lsb-release' 'python2-libgnome' 'gnome-python-desktop' 'python2-wader' 'python2-messaging' 'python2-m2crypto' 'python2-dateutil')
# check dependencies, copare with debian package
# python2-glade2
install=v-mobile-broadband.install
source=("https://github.com/andrewbird/vodafone-mobile-broadband/archive/${pkgver}.tar.gz")
sha512sums=('25bdc76e9ce51532a545b306b91423ebb3aa3146e8a251e8e0c972a600a64142fd51b52ab677b54cfabacc33c03b4ac9759090d3963fbde1ca12e1a49a2ca097')

prepare() {
  cd $srcdir/vodafone-mobile-broadband-$pkgver
  sed -i '148s/^/#/' setup.py
  sed -i '79s/^/#/' setup.py
  sed -i '88,94s/^/#/' setup.py
  sed -i '79i\ \ \ \ sub_commands = _build.sub_commands' setup.py
  sed -i '1s/python/python2/' bin/$pkgname
}

package() {
  cd $srcdir/vodafone-mobile-broadband-$pkgver

  mkdir -p $pkgdir/usr/share/$pkgname/resources
  python2 setup.py install \
    --root=$pkgdir \
    #--install-lib=$pkgdir/usr/share/$pkgname

  # Install icon and .desktop files
  install -Dm644 resources/desktop/${pkgname}.desktop "$pkgdir/usr/share/applications/${pkgname}.desktop"
  install -Dm644 resources/desktop/${pkgname}.png "$pkgdir/usr/share/pixmaps/${pkgname}.png"

  # Installing man page
  install -Dm644 resources/man/${pkgname}.1 "${pkgdir}/usr/share/man/man1/${pkgname}.1"

  # Install dbus config
  install -Dm644 resources/dbus/${pkgname}.conf "${pkgdir}/etc/dbus-1/system.d/${pkgname}.conf"

  # Install binary
  install -Dm755 bin/${pkgname} "${pkgdir}/usr/bin/${pkgname}"

  cp -rv resources/glade $pkgdir/usr/share/$pkgname/resources/ 

  # Installation for po files missing?
}
