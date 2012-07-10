# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik
pkgver=2.0.1
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
            'python-imaging:  Web Map Service'
            'python-nose:     Web Map Service'
            'apache:          Web Map Service'
            'mod_fastcgi:     Web Map Service - or:'
            'mod_fcgid:       Web Map Service - or:'
            'mod_wsgi:        Web Map Service')
makedepends=('scons' 'boost')
install="mapnik.install"
source=("https://github.com/downloads/mapnik/mapnik/mapnik-v$pkgver.tar.bz2")
md5sums=('e3dd09991340e2568b99f46bac34b0a8')

build() {
  cd "$srcdir/$pkgname-v$pkgver"
  sed -i 's|lib64|lib|g' SConstruct
  scons configure \
    PREFIX="/usr" \
    INPUT_PLUGINS=all \
    DESTDIR="$pkgdir"
  scons
}

package(){
  cd "$srcdir/$pkgname-v$pkgver"
  scons install
}
