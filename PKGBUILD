# Maintainer: Paulo Diovani <paulo@diovani.com>

pkgname=globalprotect-ui
pkgver=6.0.0.1_44
pkgrel=2
pkgdesc="Global Protect VPN Linux Client (GUI Version)"
arch=('any')
url='http://paloaltonetworks.com'
#license=('')
depends=('qt5-webkit>=5.9.1')
optdepends=('icu71: International Components for Unicode library (version 71)')
options=(!emptydirs)
install="${pkgname}.install"
source=(
  "GlobalProtect_UI_tar-${pkgver//_/-}.tgz"
)
sha256sums=(
  '833640b978861fd4333a2c86b029b35c67983f791e52d9b7df2af5c50638839a'
)

package() {
  APPDIR="${pkgdir}/usr/share/applications"
  BINDIR="${pkgdir}/usr/bin"
  GPDIR="${pkgdir}/opt/paloaltonetworks/globalprotect"
  ICONDIR="${pkgdir}/usr/share/icons/hicolor/48x48/apps"
  MANDIR="${pkgdir}/usr/share/man"
  SRVDIR="${pkgdir}/usr/lib/systemd/system"
  USRSRVDIR="${pkgdir}/usr/lib/systemd/user"

  mkdir -m 755 -p $APPDIR
  mkdir -m 755 -p $BINDIR
  mkdir -m 755 -p $GPDIR
  mkdir -m 755 -p $ICONDIR
  mkdir -m 755 -p $MANDIR
  mkdir -m 755 -p $SRVDIR
  mkdir -m 755 -p $USRSRVDIR

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
  cp -f PanMSInit.sh pre_exec_gps.sh gpshow.sh gp_support.sh uninstall.sh  $GPDIR/
  cp -f globalprotect.1.gz $MANDIR/man1

  # install services
  cp -f gpd.service $SRVDIR/
  cp -f gpa.service $USRSRVDIR/

  # add desktop entry for autostart
  if [ -f PanGPUI.desktop ]; then
    cp -f PanGPUI.desktop $GPDIR/
  fi

  # add desktop entry for mimetype
  if [ -f gp.desktop ]; then
    cp -f gp.desktop $APPDIR/
  fi

  # Add desktop entry for app menu
  if [ -f globalprotect.desktop ]; then
    cp -f globalprotect.png $GPDIR/
    cp -f globalprotect.desktop $APPDIR/
  fi

  if [ -f globalprotect.png ]; then
      cp -f globalprotect.png $ICONDIR/
  fi

  # Ensure symbol link for GPI
  ln -s ${GPDIR//$pkgdir/}/globalprotect $BINDIR/globalprotect
}

# vim:set ts=2 sw=2 et:
