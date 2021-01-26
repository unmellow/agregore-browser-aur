# Maintainer: Unmellow <name2020@googlemail.commerce>
_pkgname=agregore-browser
pkgname=agregore-browser-git
pkgver=v1.0.0.30.r3.gdc755dc
pkgrel=1
pkgdesc="A minimal browser for the distributed web"
arch=(any)
url="https://github.com/AgregoreWeb/agregore-browser"
license=(AGPL)
makedepends=('git' 'npm')
depends=('python3' 'nodejs' 'gtk3' 'libsodium' 'nss' 'lib32-gcc-libs')
source=("git+https://github.com/AgregoreWeb/agregore-browser/"
        "agregore-browser.desktop"
        "agregore-browser.sh")
sha1sums=('SKIP'
          'bf681827deb139cf7e72710bb82e1ee05ff0ef22'
          'c9c0b7e90f70a3e8b4a72ae0bc47253aafe529ed')

build() {
  cd ${srcdir}/${_pkgname}
  npm install 
  ./rebuild.sh
  npm run builder
}


pkgver() {
  cd ${srcdir}/${_pkgname}
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g'
}

package() {
  ### builded
  install -d          ${pkgdir}/usr/share/agregore-browser
  cp -r               ${srcdir}/${_pkgname}/release/linux-unpacked/*  ${pkgdir}/usr/share/agregore-browser/

  ### tools
  install -Dm644      ${srcdir}/agregore-browser.desktop             ${pkgdir}/usr/share/applications/agregore-browser.desktop
  install -Dm755      ${srcdir}/agregore-browser.sh                     ${pkgdir}/usr/bin/agregore-browser

  ### LICENSE
  install -Dm644      "${_pkgname}/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}

# vim:set ts=2 sw=2 et:
