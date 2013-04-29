# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik
pkgver=2.1.0
pkgrel=10
pkgdesc="Free Toolkit for developing mapping applications. Above all Mapnik is about rendering beautiful maps"
arch=('i686' 'x86_64')
url="http://mapnik.org/"
license=('LGPL')
depends=('boost-libs' 'icu' 'libpng' 'libjpeg' 'libtiff' 'freetype2'
	 'libxml2' 'python2' 'proj' 'cairo' 'cairomm' 'pycairo'
	 'postgresql-libs' 'postgis' 'gdal' 'curl' 'libltdl')
optdepends=('libxslt:         Web Map Service'
            'python2-lxml:    Web Map Service'
            'python-imaging:  Web Map Service'
            'python-nose:     Web Map Service'
            'apache:          Web Map Service'
            'mod_fastcgi:     Web Map Service - or:'
            'mod_fcgid:       Web Map Service - or:'
            'mod_wsgi2:       Web Map Service')
makedepends=('scons' 'boost')
install="mapnik.install"
source=("https://github.com/downloads/mapnik/mapnik/mapnik-v$pkgver.tar.bz2"
        "mapnik-2.1.0-compile-fix-for-boost-1.53.patch")
md5sums=('d580c558a957444873bec9e24526b0a0'
         'fb456216b052742319428f65f1c979d6')

build() {
  cd "$srcdir/$pkgname-v$pkgver"

  # https://github.com/mapnik/mapnik/issues/1658
  patch -Np1 -i "$srcdir/mapnik-2.1.0-compile-fix-for-boost-1.53.patch"

  sed -i 's|lib64|lib|g' SConstruct
  sed -i 's|python|python2|' \
	utils/performance/mapnik-speed-check \
	utils/upgrade_map_xml/*.py
  scons configure \
    PREFIX="/usr" \
    INPUT_PLUGINS=all \
    DESTDIR="$pkgdir"
  scons $MAKEFLAGS
}

package(){
  cd "$srcdir/$pkgname-v$pkgver"
  scons install
}
