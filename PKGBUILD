# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik
pkgver=0.7.1
pkgrel=8
pkgdesc="Free Toolkit for developing mapping applications. Above all Mapnik is about rendering beautiful maps."
arch=('i686' 'x86_64')
url="http://mapnik.org/"
license=('LGPL')
depends=('boost-libs' 'icu' 'libpng' 'libjpeg' 'libtiff' 'freetype2'
	 'libxml2' 'python2' 'proj' 'cairo' 'cairomm' 'pycairo'
	 'postgresql-libs' 'postgis' 'gdal' 'curl' 'libtool')
	# already in core ('zlib' 'sqlite3')
optdepends=('libxslt:         Web Map Service'
            'python-lxml:     Web Map Service'
            'python-imaging:  Web Map Service'
            'python-nose:     Web Map Service'
            'apache:          Web Map Service'
            'mod_fastcgi:     Web Map Service - or:'
            'mod_fcgid:       Web Map Service - or:'
            'mod_wsgi:        Web Map Service'
           )
makedepends=('scons' 'boost') # already in core ('pkg-config')
conflicts=('mapnik-svn')
install="mapnik.install"
source=("http://download.berlios.de/${pkgname}/${pkgname}-${pkgver}.tar.bz2")
md5sums=('8f65fda2a792518d6f6be8a85f62fc73')

build() {
  cd "$srcdir/$pkgname-$pkgver"

  #patch SConstruct so libs end up in /usr/lib not /usr/lib64 on X86_64
  sed -i -e "/LIBDIR_SCHEMA=/s/lib64/lib/" SConstruct

  sed -i 's/-ansi -Wall/-ansi -DBOOST_FILESYSTEM_VERSION=2 -Wall/' SConstruct

  scons configure \
    PREFIX="/usr" \
    INPUT_PLUGINS=all \
    DESTDIR="$pkgdir"
  scons
  scons install

  # fix permissions on SCons-autogenerated files
  chmod 644 "${pkgdir}/usr/lib/python2.7/site-packages/mapnik/paths.py"
}
