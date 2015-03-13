# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik
pkgver=2.2.0.654.g718a8b3
pkgrel=1
pkgdesc="Free Toolkit for developing mapping applications. Above all Mapnik is about rendering beautiful maps"
arch=('i686' 'x86_64')
url="http://mapnik.org/"
license=('LGPL')
depends=('boost-libs' 'icu' 'libpng' 'libjpeg' 'libtiff' 'freetype2'
	 'libxml2' 'python2' 'proj' 'cairo' 'cairomm' 'pycairo'
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
#source=("$pkgname-$pkgver.tar.gz::https://github.com/mapnik/mapnik/archive/v$pkgver.tar.gz")
source=("git://github.com/mapnik/mapnik.git#branch=2.3.x")
md5sums=('SKIP')

pkgver() {
  cd "$srcdir/$pkgname"

  git describe --long | cut -c2- | sed 's/-/./g'
}

build() {
  cd "$srcdir/$pkgname"

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
  cd "$srcdir/$pkgname"
  scons install
}
