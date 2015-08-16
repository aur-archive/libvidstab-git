# Maintainer: Naofumi Hattori <hattorix0@gmail.com>

pkgname=libvidstab-git
pkgver=4ec5be1
pkgrel=1
pkgdesc="Transcode video stabilization plugin"
arch=('i686' 'x86_64')
url="http://public.hronopik.de/vid.stab"
license=('GPL')
makedepends=('git' 'cmake')
provides=('vid.stab')
conflicts=('vid.stab')
sha1sum=('SKIP')

_gitroot="https://github.com/georgmartius/vid.stab.git"
_gitname=libvidstab

pkgver() {
  cd $_gitname
  git describe --always | sed 's|-|.|g'
}

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  #
  # BUILD HERE
  #
  cmake . -DCMAKE_INSTALL_PREFIX=/usr
  make
}

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir/" install
}

# vim:set ts=2 sw=2 et:
