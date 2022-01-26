# Maintainer: Paulo Diovani <paulo@diovani.com>

pkgname=globalprotect-ui
pkgver=5.3.1.0_36
pkgrel=2
pkgdesc="Global Protect VPN Linux Client (GUI Version)"
arch=('any')
url='http://paloaltonetworks.com'
#license=('')
depends=('qt5-webkit>=5.9.1')
options=(!emptydirs)
install="${pkgname}.install"
source=(
  "GlobalProtect_UI_tar-${pkgver//_/-}.tgz"
  'gpa.service'
  'globalprotect.desktop'
  'globalprotect.png'
)
sha256sums=(
  '387e5dc03eb7eb2ba9de4a8e3421ef2a6cf00dbd205e4b01ea0741a1311e9f1e'
  '3556c8c5df9c086cdfdece0fa96020828d587957bcb800b396d77891d4f72a99'
  '7c26591a646b647e540c562c58d8717ed76a6b25c0ae78eced8c8986f9f7fb90'
  '79cc793192519579ea7628cc6ab49207c72040d4e5dc25b37e200b604f87a771'
)

package() {
  MANDIR="${pkgdir}/usr/share/man"
  SRVDIR="${pkgdir}/usr/lib/systemd/system"
  USRSRVDIR="${pkgdir}/usr/lib/systemd/user"
  BINDIR="${pkgdir}/usr/bin"
  APPDIR="${pkgdir}/usr/share/applications"
  GPDIR="${pkgdir}/opt/paloaltonetworks/globalprotect"

  mkdir -m 755 -p $MANDIR
  mkdir -m 755 -p $SRVDIR
  mkdir -m 755 -p $USRSRVDIR
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

  # add desktop entry for autostart
  if [ -f PanGPUI.desktop ]; then
    cp -f PanGPUI.desktop $GPDIR/
  fi

  cp -df *.so* $GPDIR/
  cp -f license.cfg $GPDIR/
  cp -f PanMSInit.sh pre_exec_gps.sh gpshow.sh gp_support.sh uninstall.sh  $GPDIR/
  cp -f globalprotect.1.gz $MANDIR/man1

  # install services
  cp -f gpd.service $SRVDIR/
  cp -f gpa.service $USRSRVDIR/

  # Ensure symbol link for GPI
  ln -s ${GPDIR//$pkgdir/}/globalprotect $BINDIR/globalprotect

  # Add desktop entry for app menu
  cp -f globalprotect.png $GPDIR/
  cp -f globalprotect.desktop $APPDIR/

  # add desktop entry for mimetype
  if [ -f gp.desktop ]; then
    cp -f gp.desktop $APPDIR/
  fi
}

# vim:set ts=2 sw=2 et:
