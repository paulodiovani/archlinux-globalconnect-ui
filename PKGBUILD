# Maintainer: Paulo Diovani <paulo@diovani.com>

pkgname=globalprotect-ui
pkgver=5.1.1.0_17
pkgrel=1
pkgdesc="Global Protect VPN Linux Client (GUI Version)"
arch=('any')
url='http://paloaltonetworks.com'
#license=('')
depends=('qt5-webkit>=5.9.1')
options=(!emptydirs)
install="${pkgname}.install"
# source=("GlobalProtect_tar-${pkgver//_/-}.tgz")
# sha256sums=('48df5b667ed2bcd7b5367b5feac73f898db73443933380c5d31d23148bdc752c')
source=("GlobalProtect_UI_tar-${pkgver//_/-}.tgz")
sha256sums=('60ae137b5f12150c9c5ba6f2efd0fcb1d4bfa067c68261e156ff19cc586487d0')

package() {
  MANDIR="${pkgdir}/usr/share/man"
  SRVDIR="${pkgdir}/usr/lib/systemd/system"
  BINDIR="${pkgdir}/usr/bin"
  APPDIR="${pkgdir}/usr/share/applications"
  GPDIR="${pkgdir}/opt/paloaltonetworks/globalprotect"

  mkdir -m 755 -p $MANDIR
  mkdir -m 755 -p $SRVDIR
  mkdir -m 755 -p $BINDIR
  mkdir -m 755 -p $APPDIR
  mkdir -m 755 -p $GPDIR

  cd "${srcdir}"

  # install files
  if [ -d release ]; then
    cp -f release/* $GPDIR/
  else
    cp -f globalprotect PanGPA PanGPS PanGpHip PanGpHipMp $GPDIR/
    if [ -f PanGPUI ]; then
        cp -f PanGPUI $GPDIR/
    fi
  fi

  cp -df *.so* $GPDIR/
  cp -f license.cfg $GPDIR/
  cp -f gpd gpd.service pangps.xml $GPDIR/
  cp -f PanMSInit.sh pre_exec_gps.sh gpshow.sh gp_support.sh uninstall.sh  $GPDIR/
  cp -f gpui_apt_dep.sh gpui_yum_dep.sh $GPDIR/
  cp -f globalprotect.1.gz $MANDIR/man1

  if [ -f PanGPUI.desktop ]; then
    cp -f PanGPUI.desktop $GPDIR/
  fi

  # install service
  cp $GPDIR/gpd.service $SRVDIR/gpd.service

  # Ensure symbol link for GPI
  ln -s ${GPDIR//$pkgdir/}/globalprotect $BINDIR/globalprotect

  # add desktop entry
  cp $GPDIR/PanGPUI.desktop $APPDIR/
}

# vim:set ts=2 sw=2 et:
