# Maintainer: sudokode <sudokode@gmail.com>
# Previous Maintainer: Crass00 <crass00 at hotmail dot com>
# Previous Maintainer: Superstar655 <choman000 at hotmail dot com>
# Contributor: Augusto Born de Oliveira <augustoborn at gmail dot com>

pkgname=sickbeard-git
pkgver=alpha1.r3478.g79cb8f2
pkgrel=1
pkgdesc="A PVR application that downloads and manages your TV shows"
arch=('any')
url="http://code.google.com/p/sickbeard/"
license=('GPL3')
depends=('python2' 'python2-cheetah')
makedepends=('git')
optdepends=('sabnzbd: NZB downloader'
            'python2-pyopenssl: enable ssl'
            'python2-notify: desktop notifications')
install=sickbeard.install
conflicts=('sickbeard')
source=("$pkgname::git://github.com/midgetspy/Sick-Beard.git"
        'sickbeard-system.service' 'sickbeard-user.service' 'sickbeard.tmpfile')
sha256sums=('SKIP'
            'aa2b6496bf622d2b235a47b80d950ba84411e879a08bc656d227e224653aeded'
            'bf2f9792d3d7e1d703fec9bf61a1562a34b8d08d1dba3d560e6299ea25bd5a72'
            '24f20de2445ff3998aad5d87d94e0fea3b22eb1d0a451ed33ec301ac36a7398d')

pkgver() {
  cd $pkgname

  git describe --tags | sed 's/\([^-]*-g\)/r\1/; s/-/./g'
}

prepare() {
  cd $pkgname

  # Fix python2 shebang
  sed -i 's/python/python2/g' autoProcessTV/sabToSickBeard.py
  sed -i 's/python/python2/g' autoProcessTV/hellaToSickBeard.py
}

package() {
  mkdir -p "$pkgdir"/opt/sickbeard
  chmod 775 "$pkgdir"/opt/sickbeard
  cp -r $pkgname/* "$pkgdir"/opt/sickbeard

  install -D -m644 sickbeard-system.service "$pkgdir"/usr/lib/systemd/system/sickbeard.service
  install -D -m644 sickbeard-user.service "$pkgdir"/usr/lib/systemd/user/sickbeard.service
  install -D -m644 sickbeard.tmpfile "$pkgdir"/usr/lib/tmpfiles.d/sickbeard.conf
}

# vim:set ts=2 sw=2 et:
