# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: Jaroslav Lichtblau <svetlemodry@archlinux.org>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik
pkgver=3.0.13
pkgrel=5
pkgdesc="Free Toolkit for developing mapping applications. Above all Mapnik is about rendering beautiful maps"
arch=('i686' 'x86_64')
url="http://mapnik.org/"
license=('LGPL')
depends=('boost-libs' 'icu' 'libpng' 'libjpeg' 'libtiff' 'freetype2'
	 'libxml2' 'python2' 'proj' 'cairo' 'cairomm' 'python2-cairo'
	 'postgresql-libs' 'postgis' 'gdal' 'curl' 'libltdl')
optdepends=('libxslt:         Web Map Service'
            'python2-lxml:    Web Map Service'
            'python2-pillow:  Web Map Service'
            'python-nose:     Web Map Service'
            'apache:          Web Map Service'
            'mod_fastcgi:     Web Map Service - or:'
            'mod_fcgid:       Web Map Service - or:'
            'mod_wsgi2:       Web Map Service')
makedepends=('scons' 'boost' 'git')
install="mapnik.install"
source=("https://github.com/$pkgname/$pkgname/releases/download/v$pkgver/$pkgname-v$pkgver.tar.bz2"
        'icu59.patch')
sha256sums=('d6213d514a0e3cd84d9bfcb6d97208d169ffcaae1f36250f6555655cdfe57bcc'
            'b391a775f28ec9bc7d5d2a8ef429789d8c6158bdf8023f395501fbfc8137cc22')

prepare() {
  cd "$srcdir/$pkgname-v$pkgver"
  patch -Np1 -i ../icu59.patch
}

build() {
  cd "$srcdir/$pkgname-v$pkgver"
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
  cd "$srcdir/$pkgname-v$pkgver"
  scons install
}
