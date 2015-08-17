# $Id: pkgbuild-mode.el,v 1.23 2007/10/20 16:02:14 juergen Exp $
# Contributor: Sergey Mastykov <smastykov[at]gmail[dot]com>

pkgname=pycharm
pkgver=3.0
pkgrel=1
pkgdesc="Powerful Python and Django IDE. 30-day free trial."
arch=('any')
options=('!strip')
url="http://www.jetbrains.com/pycharm/"
license=('Commercial')
depends=('java-environment>=6')
source=("http://download.jetbrains.com/python/pycharm-professional-${pkgver}.tar.gz")
sha256sums=('2ef85d8fad030279408e0415d3fbeca55e3a53850198337e492bb02927b63cbf')

package() {
  cd $srcdir
  mkdir -p $pkgdir/opt/$pkgname || return 1
  cp -R $srcdir/$pkgname-$pkgver/* $pkgdir/opt/$pkgname || return 1
  if [[ $CARCH = 'i686' ]]; then
          rm -f $pkgdir/opt/$pkgname/bin/libyjpagent-linux64.so
          rm -f $pkgdir/opt/$pkgname/bin/fsnotifier64
          echo '-Dawt.useSystemAAFontSettings=on' >> $pkgdir/opt/$pkgname/bin/pycharm.vmoptions
          echo '-Dswing.aatext=true' >> $pkgdir/opt/$pkgname/bin/pycharm.vmoptions
     else
	  echo '-Dawt.useSystemAAFontSettings=on' >> $pkgdir/opt/$pkgname/bin/pycharm64.vmoptions
          echo '-Dswing.aatext=true' >> $pkgdir/opt/$pkgname/bin/pycharm64.vmoptions 
  fi

(
cat <<EOF
[Desktop Entry]
Version=$pkgver
Name=PyCharm
Icon=pycharm
GenericName=Develop with pleasure!
Comment=Powerful Python and Django IDE 30-day free trial
Exec=/opt/$pkgname/bin/pycharm.sh
Terminal=false
Type=Application
Categories=Development
EOF
) > $startdir/pycharm.desktop

  mkdir -p $pkgdir/usr/share/applications/ || return 1
  mkdir -p $pkgdir/usr/share/pixmaps/ || return 1
  mkdir -p $pkgdir/usr/share/licenses/$pkgname/ || return 1
  install -Dm644 $startdir/pycharm.desktop $pkgdir/usr/share/applications/
  install -Dm644 $pkgdir/opt/$pkgname/bin/pycharm.png $pkgdir/usr/share/pixmaps/pycharm.png
  install -Dm644 $srcdir/$pkgname-$pkgver/license/PyCharm_license.txt $pkgdir/usr/share/licenses/$pkgname/PyCharm_license.txt
}

# vim:set ts=2 sw=2 et:
