# Maintainer: Amadiro <jwringstad@gmail.com>

# This package builds and installs a stand-alone, developmental version of
# Krita which conflicts with most or all of the Calligra suite found in
# the extra repository.

pkgname=krita-git
_pkgname=calligra
pkgver=96506.e300230
pkgrel=1
pkgdesc="Digital painting and illustration suite (stand-alone)."
arch=('i686' 'x86_64')
url="http://www.krita.org/"
license=('GPL2')
depends=('eigen' 'exiv2' 'fftw' 'glew' 'kdebase-runtime' 'libkdcraw'
         'libpng' 'opencolorio' 'gsl')
makedepends=('automoc4' 'boost' 'cmake' 'git' 'lcms2' 'openjpeg' 'vc')
provides=('calligra-krita')
conflicts=('calligra-krita' 'calligra-plugins' 'calligra-libs' 'calligra-extras', 'calligra-filters')
install=krita.install
source=("$_pkgname::git://anongit.kde.org/calligra#branch=calligra/2.9")
sha256sums=('SKIP')

pkgver() {
  cd "$srcdir/$_pkgname"
  # necessary, otherwise the --count will fail
  git checkout "calligra/2.9" > /dev/null 2>&1
  echo $(git rev-list --count 'calligra/2.9').$(git rev-parse --short 'calligra/2.9')
}

prepare() {
  cd "$srcdir/$_pkgname"
    
  # You can delete src/calligra/krita-build/
  # if you want to build completely from scratch
  # (seems that is occasionally necessary when
  # the upstream krita devs change the makefile)

  mkdir -p krita-build
}

build() {
    cd "$srcdir/$_pkgname/krita-build"
  cmake ../ \
    -DCMAKE_BUILD_TYPE=Release \
    -DPRODUCTSET=KRITA \
    -DCMAKE_INSTALL_PREFIX=/usr \
    -DCMAKE_INSTALL_LIBDIR=/usr/lib \
    -Wno-dev
  make #   -DLIB_INSTALL_DIR=/usr/lib \
}

package() {
  cd "$srcdir/$_pkgname/krita-build"
  make DESTDIR="$pkgdir" install
}
