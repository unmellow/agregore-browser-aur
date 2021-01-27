# Maintainer: Unmellow <name2020@googlemail.commerce>
_pkgname=agregore-browser
pkgname=agregore-browser-git
pkgver=1.0.0.30.r3.gdc755dc
pkgrel=1
pkgdesc="A minimal browser for the distributed web"
arch=('x86_64')
url="https://github.com/AgregoreWeb/agregore-browser"
license=(AGPL)
makedepends=('git' 'npm')
depends=('python3' 'nodejs' 'gtk3' 'libsodium' 'nss' 'lib32-gcc-libs')
source=("git+https://github.com/AgregoreWeb/agregore-browser/"
        "agregore-browser.desktop"
        "agregore-browser.sh")
sha1sums=('SKIP'
          '0b98e3f505a0c6d4eafa3d8a8f2b1cf65d66d501'
          'ee8474defb6d3dd06b734589e45ca5bdddc047e2')

build() {
  cd "${srcdir}/${_pkgname}"
  npm install 
  npm run builder
}


pkgver() {
  cd ${srcdir}/${_pkgname}
  git describe --long --tags | sed 's/\([^-]*-g\)/r\1/;s/-/./g' | sed 's/^v//'
}

package() {
  ### builded
  install -d          "${pkgdir}/usr/lib/agregore-browser"
  cp -r               "${srcdir}/${_pkgname}/"release/linux-unpacked/*  "${pkgdir}/usr/lib/agregore-browser/"

  ### tools
  install -Dm644      "${srcdir}/agregore-browser.desktop"              "${pkgdir}/usr/share/applications/agregore-browser.desktop"
  install -Dm755      "${srcdir}/agregore-browser.sh"                   "${pkgdir}/usr/bin/agregore-browser"

  ### LICENSE
  install -Dm644      "${_pkgname}/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE" 

} 
# vim:set ts=2 sw=2 et:
