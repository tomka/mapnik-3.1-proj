# Maintainer: Jaroslav Lichtblau <svetlemodry@archlinux.org>
# Contributor: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik
pkgver=3.0.17
pkgrel=1
pkgdesc="Free Toolkit for developing mapping applications and rendering beautiful maps"
arch=('x86_64')
url="http://mapnik.org/"
license=('LGPL')
depends=('boost-libs' 'icu' 'libpng' 'libjpeg-turbo' 'libtiff' 'freetype2'
         'libxml2' 'python2' 'proj' 'cairo' 'cairomm' 'python2-cairo'
         'postgresql-libs' 'postgis' 'gdal' 'curl' 'libtool')
makedepends=('scons' 'boost' 'git')
optdepends=('libxslt:         Web Map Service'
            'python2-lxml:    Web Map Service'
            'python2-pillow:  Web Map Service'
            'python-nose:     Web Map Service'
            'apache:          Web Map Service'
            'mod_fcgid:       Web Map Service - or:'
            'mod_wsgi2:       Web Map Service')
install=$pkgname.install
source=(https://github.com/$pkgname/$pkgname/releases/download/v$pkgver/$pkgname-v$pkgver.tar.bz2)
sha256sums=('5ccd2ba7b82ca00028c6ce3ae5856b41d6f658217b680288f14b9c416d17ccb2')

build() {
  cd "${srcdir}"/$pkgname-v$pkgver

  PYTHON=python2
  scons configure \
    PREFIX="/usr" \
    INPUT_PLUGINS=all \
    XMLPARSER=libxml2 \
    DESTDIR="$pkgdir" \
    CUSTOM_CXXFLAGS="-DBOOST_OPTIONAL_CONFIG_USE_OLD_IMPLEMENTATION_OF_OPTIONAL"
  scons -j1 # $MAKEFLAGS
}

package(){
  cd "${srcdir}"/$pkgname-v$pkgver
  scons install
}
