# Maintainer: Ner0

pkgname=mundus-bzr
pkgver=487
pkgrel=1
pkgdesc="Clean and backup your /home and /etc folder from old configuration files once created by uninstalled software."
arch=('any')
url="https://launchpad.net/mundus"
license=('GPL3')
depends=('gambas3-gb-crypt' 'gambas3-gb-desktop' 'gambas3-gb-form' 'gambas3-gb-form-stock'
         'gambas3-gb-image' 'gambas3-gb-net' 'gambas3-gb-net-curl' 'gambas3-gb-qt4'
         'gambas3-gb-settings' 'gambas3-gb-web' 'gambas3-runtime' 'gambas3-gb-option')
makedepends=('bzr' 'gambas3-devel')
provides=('mundus')
conflicts=('mundus')

_bzrtrunk=lp:mundus
_bzrmod=mundus

build() {
  msg "Connecting to Bazaar server...."

  if [[ -d "$_bzrmod" ]]; then
    cd "$_bzrmod" && bzr pull "$_bzrtrunk" -r $pkgver && cd ..
    msg "The local files are updated."
  else
    bzr branch "$_bzrtrunk" "$_bzrmod" -r $pkgver
  fi

  msg "BZR checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$_bzrmod-build"
  cp -r "$_bzrmod" "$_bzrmod-build"
  cd "$_bzrmod-build"

  make
}

package() {
  cd "$_bzrmod-build"
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
