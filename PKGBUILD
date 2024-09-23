# Maintainer: Tom Kazimiers <tom@voodoo-arts.net>
# Contributor: Jaroslav Lichtblau <svetlemodry@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik-3.1-proj
pkgver=3.1.0
pkgrel=2
pkgdesc="Free Toolkit for developing mapping applications and rendering beautiful maps. Compiled with Proj support."
arch=('x86_64')
provides=('mapnik=3.1.0')
url="https://mapnik.org/"
license=('LGPL')
depends=('boost-libs' 'cairo' 'freetype2' 'gdal' 'harfbuzz' 'icu' 'libjpeg-turbo' 'libpng'
         'libtiff' 'libwebp' 'libxml2' 'postgresql-libs' 'proj' 'sqlite' 'zlib')
conflicts=('mapnik' 'mapnik-git')
makedepends=('boost' 'scons')
source=(https://github.com/mapnik/mapnik/releases/download/v$pkgver/mapnik-v$pkgver.tar.bz2
        boost-1.80.patch
        scons4.patch
        gcc-13.patch
        boost-1.83.patch
        libxml2-2.12.patch
        mapnik-gcc14.patch
        proj.patch
        boost-1.85.patch)
sha256sums=('43d76182d2a975212b4ad11524c74e577576c11039fdab5286b828397d8e6261'
            'b80085fba71ea6ecd86ff98ebdf652490bf56507cb798076192ab3ce136f5eeb'
            '79a85ddba3ec17b86cb216e21442611498a9f2612f03e98708057b3c3a6e8b06'
            '84ddba271d74fd4ed1d26501789c50c5e6bda509c238986eb69f96b10cf1465a'
            '356271f4550c2b370ae48bbce9cebb58c5803507f2b14bc8e84f3813871d0645'
            'f56d43aab85750505d56aa92f8f34453f4344e76a7ccdf394e874245b05990c3'
            '086c57f5907c2e3f378f1f747dce59cf7ce5e5cffdd7c3779414dab2405eaed2'
            '567512661a0601691335cb7defc5c156ba2c37c82cc5b2056a547c4f473876a9'
            '23c26604fd191459da70aa29fc9cf6578e0f3ca75c9240150b3f2247d92cb070')

prepare() {
  cd "${srcdir}"/mapnik-v$pkgver
  patch -Np1 -i ../boost-1.80.patch

  # Partial fix to build with SCons 4 (https://bugs.archlinux.org/task/71630)
  patch -Np1 -i ../scons4.patch

  # Fix build with GCC 13
  patch -p1 -i ../gcc-13.patch

  # Fix build with boost 1.83
  patch -p1 -i ../boost-1.83.patch

  # Fix build with libxml2 2.12
  patch -p1 -i ../libxml2-2.12.patch

  # Fix build with ICU 75
  sed -e 's|c++14|c++17|' -i SConstruct

  # Fix build with GCC 14
  patch -p1 -i ../mapnik-gcc14.patch

  # Add Proj4 support
  patch -p1 -i ../proj.patch

  # Fix build with boost 1.85
  patch -p1 -i ../boost-1.85.patch
}

build() {
  cd "${srcdir}"/mapnik-v$pkgver
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
  cd "${srcdir}"/mapnik-v$pkgver
  scons install
}
