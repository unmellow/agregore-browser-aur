# Maintainer: Unmellow <amazingminecrafter2015 at gmail dot com>
# shellcheck shell=bash disable=SC2034,SC2154
#
# AUR already has agregore-browser-bin. This is the source/-git variant
# using the system Electron (wiki Electron package guidelines).

_pkgname=agregore-browser
pkgname=agregore-browser-git
pkgver=1.0.0.30.r6.gc78b34b
pkgrel=2
pkgdesc="A minimal browser for the distributed web"
arch=('x86_64')
url="https://github.com/AgregoreWeb/agregore-browser"
license=('AGPL-3.0-or-later')
depends=('electron' 'libsodium')
makedepends=('git' 'npm' 'python')
provides=("agregore-browser=${pkgver}")
conflicts=('agregore-browser' 'agregore-browser-bin')
options=('!strip' '!debug')
source=("${_pkgname}::git+https://github.com/AgregoreWeb/agregore-browser.git"
        "agregore-browser.desktop"
        "agregore-browser.sh")
sha256sums=('SKIP'
            '499ec44c3b143267ae13d77b88a3daaccc64e1a5d526d017f8113b7bb6672cc3'
            'c7384b6cc580b909aa6db700996a7fdbea2a5e8f2fc3498881dafdcfd75d9aec')

pkgver() {
  cd "$_pkgname"
  git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

build() {
  cd "${srcdir}/${_pkgname}"
  local electronDist electronVer
  electronDist="$(dirname "$(realpath "$(command -v electron)")")"
  electronVer="$(electron --version)"
  electronVer="${electronVer#v}"

  HOME="${srcdir}/.electron-gyp" npm install --cache "${srcdir}/npm-cache"
  ./node_modules/.bin/electron-builder --linux --x64 --dir -p never \
    -c.electronDist="$electronDist" \
    -c.electronVersion="$electronVer"
}

package() {
  local unpacked="${srcdir}/${_pkgname}/release/linux-unpacked"
  install -d "${pkgdir}/usr/lib/${_pkgname}"
  if [[ -d "${unpacked}/resources/app" ]]; then
    cp -a "${unpacked}/resources/app/." "${pkgdir}/usr/lib/${_pkgname}/"
  elif [[ -f "${unpacked}/resources/app.asar" ]]; then
    install -d "${pkgdir}/usr/lib/${_pkgname}/resources"
    install -Dm644 "${unpacked}/resources/app.asar" \
      "${pkgdir}/usr/lib/${_pkgname}/resources/app.asar"
  else
    echo "neither resources/app nor app.asar found" >&2
    return 1
  fi

  install -Dm644 "${srcdir}/agregore-browser.desktop" \
    "${pkgdir}/usr/share/applications/agregore-browser.desktop"
  install -Dm755 "${srcdir}/agregore-browser.sh" \
    "${pkgdir}/usr/bin/agregore-browser"

  local icon
  icon=$(find "${srcdir}/${_pkgname}" -path '*node_modules*' -prune -o -name 'icon.png' -print | head -n1)
  [[ -n "$icon" ]] && install -Dm644 "$icon" \
    "${pkgdir}/usr/share/pixmaps/agregore-browser.png"

  install -Dm644 "${_pkgname}/LICENSE" "${pkgdir}/usr/share/licenses/${pkgname}/LICENSE"
}
