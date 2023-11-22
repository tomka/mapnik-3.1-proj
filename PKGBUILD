# Maintainer: Jaroslav Lichtblau <svetlemodry@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik-3.1
pkgver=3.1.0
pkgrel=1
pkgdesc="Free Toolkit for developing mapping applications and rendering beautiful maps, with Proj4 support"
arch=('x86_64')
url="https://mapnik.org/"
license=('LGPL')
depends=('boost-libs' 'cairo' 'freetype2' 'gdal' 'harfbuzz' 'icu' 'libjpeg-turbo' 'libpng'
         'libtiff' 'libwebp' 'libxml2' 'postgresql-libs' 'proj' 'sqlite' 'zlib')
makedepends=('boost' 'scons')
source=(https://github.com/$pkgname/$pkgname/releases/download/v$pkgver/$pkgname-v$pkgver.tar.bz2
        boost-1.80.patch
        scons4.patch
        gcc-13.patch
        boost-1.83.patch
        proj.patch)
sha256sums=('43d76182d2a975212b4ad11524c74e577576c11039fdab5286b828397d8e6261'
            'b80085fba71ea6ecd86ff98ebdf652490bf56507cb798076192ab3ce136f5eeb'
            '79a85ddba3ec17b86cb216e21442611498a9f2612f03e98708057b3c3a6e8b06'
            '84ddba271d74fd4ed1d26501789c50c5e6bda509c238986eb69f96b10cf1465a'
            '356271f4550c2b370ae48bbce9cebb58c5803507f2b14bc8e84f3813871d0645'
            '567512661a0601691335cb7defc5c156ba2c37c82cc5b2056a547c4f473876a9')

prepare() {
  cd "${srcdir}"/$pkgname-v$pkgver
  patch -Np1 -i ../boost-1.80.patch

  # Partial fix to build with SCons 4 (https://bugs.archlinux.org/task/71630)
  patch -Np1 -i ../scons4.patch

  # Fix build with GCC 13
  patch -p1 -i ../gcc-13.patch

  # Fix build with boost 1.83
  patch -p1 -i ../boost-1.83.patch

  # Add Proj4 support
  patch -p1 -i ../proj.patch
}

build() {
  cd "${srcdir}"/$pkgname-v$pkgver
  scons configure  FAST=True \
    PREFIX="/usr" \
    INPUT_PLUGINS=all \
    XMLPARSER=libxml2 \
    DESTDIR="$pkgdir" \
    CUSTOM_CXXFLAGS="$CXXFLAGS -ffat-lto-objects" \
    CUSTOM_LDFLAGS="$LDFLAGS" \
    CUSTOM_DEFINES="-DMAPNIK_USE_PROJ4"
  scons $(expr "$MAKEFLAGS" : '.*\(\-j[0-9]\+\)')
}

package(){
  cd "${srcdir}"/$pkgname-v$pkgver
  scons install
}
