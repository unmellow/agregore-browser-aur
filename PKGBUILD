# Maintainer: Unmellow <name2020@googlemail.commerce>
_pkgname=agregore-browser
pkgname=agregore-browser-git
pkgver=1.0.0.30.r6.gc78b34b
pkgrel=1
pkgdesc="A minimal browser for the distributed web"
arch=('x86_64')
url="https://github.com/AgregoreWeb/agregore-browser"
license=(AGPL)
makedepends=('git' 'npm')
depends=('electron' 'python3' 'nodejs' 'libsodium')
source=("git+https://github.com/AgregoreWeb/agregore-browser/"
        "agregore-browser.desktop"
        "agregore-browser.sh")
sha1sums=('SKIP'
          '5df84e15aba60d304d0fa102d78b797a737718f3' 
          'b2d858eb3b8d716fff8ef3e40bef3219cb26140b')
pkgver() {
  cd "$_pkgname"
  # cutting off 'v' prefix that presents in the git tag
  git describe --long | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${srcdir}/${_pkgname}"
  # use system electron version
  # see: https://wiki.archlinux.org/index.php/Electron_package_guidelines
  electronDist=$(dirname $(realpath $(which electron)))
  electronVer=$(electron --version | tail -c +2)
  sed -i '/		"electron": /d' ./package.json
  HOME="$srcdir/.electron-gyp" npm install --cache "${srcdir}/npm-cache"
  ./node_modules/.bin/electron-builder --linux --x64 -c.electronDist=$electronDist -c.electronVersion=$electronVer --dir
} 


package() {
  ### built
  install -d          "${pkgdir}/usr/lib/agregore-browser"
  cp -r               "${srcdir}/${_pkgname}/"release/linux-unpacked/*  "${pkgdir}/usr/lib/agregore-browser/"

  # find "${pkgdir}/usr/lib/agregore-browser/" -iname "macos"            -exec rm -rf {} \; || true
  find "${pkgdir}/usr/lib/agregore-browser/" -iname "*-arm*"           -exec rm -rf {} \; || true 
  find "${pkgdir}/usr/lib/agregore-browser/" -iname "electron-builder" -exec rm -rf {} \; || true 
  find "${pkgdir}/usr/lib/agregore-browser/" -iname "electron"         -exec rm -rf {} \; || true  
  find "${pkgdir}/usr/lib/agregore-browser/" -iname "android-*"        -exec rm -rf {} \; || true  


  ### tools
  install -Dm644      "${srcdir}/agregore-browser.desktop"              "${pkgdir}/usr/share/applications/agregore-browser.desktop"
  install -Dm755      "${srcdir}/agregore-browser.sh"                   "${pkgdir}/usr/bin/agregore-browser"

  ### LICENSE
  install -Dm644      "${_pkgname}/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE" 

}
# vim:set ts=2 sw=2 et:
