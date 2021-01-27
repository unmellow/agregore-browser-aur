# Maintainer: Unmellow <name2020@googlemail.commerce>
_pkgname=agregore-browser
pkgname=agregore-browser-git
pkgver=1.0.0.30.r3.gdc755dc
pkgrel=1
pkgdesc="A minimal browser for the distributed web"
arch=('x86_64')
url="https://github.com/AgregoreWeb/agregore-browser"
license=(AGPL)
install=agregore-browser.install
makedepends=('git' 'npm')
depends=('electron' 'python3' 'nodejs')
source=("git+https://github.com/AgregoreWeb/agregore-browser/"
        "agregore-browser.desktop"
        "agregore-browser.sh"
        "agregore-browser.install")
sha1sums=('SKIP'
          '0b98e3f505a0c6d4eafa3d8a8f2b1cf65d66d501'
          '4b4467fef75406e8e669422b85e68c8f15b3beaf'
          'fcfae500c95434715da05756cab5ab83d70a8848')


# should we remove this?
build() {
  cd "${srcdir}/${_pkgname}"
  # npm install
}


pkgver() {
  cd "$_pkgname"
  # cutting off 'v' prefix that presents in the git tag
  git describe --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}


package() {
  ### builded
  install -d          "${pkgdir}/usr/lib/agregore-browser"
  cp -r               "${srcdir}/${_pkgname}/"app              "${pkgdir}/usr/lib/agregore-browser/"
  cp -r               "${srcdir}/${_pkgname}/"package.json     "${pkgdir}/usr/lib/agregore-browser/"
  cp -r               "${srcdir}/${_pkgname}/"build            "${pkgdir}/usr/lib/agregore-browser/"

  ### tools
  install -Dm644      "${srcdir}/agregore-browser.desktop"              "${pkgdir}/usr/share/applications/agregore-browser.desktop"
  install -Dm755      "${srcdir}/agregore-browser.sh"                   "${pkgdir}/usr/bin/agregore-browser"

  ### LICENSE
  install -Dm644      "${_pkgname}/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE" 

} 
# vim:set ts=2 sw=2 et:
