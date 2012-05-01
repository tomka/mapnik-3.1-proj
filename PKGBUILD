# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Contributor: David Dent <thewinch@gmail.com>
# Contributor: orbisvicis <orbisvicis@gmail.com>

pkgname=mapnik
pkgver=0.7.1
pkgrel=16
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
            'mod_wsgi:        Web Map Service'
           )
makedepends=('scons' 'boost')
install="mapnik.install"
source=("http://download.berlios.de/${pkgname}/${pkgname}-${pkgver}.tar.bz2"
        'gcc47.patch')
md5sums=('8f65fda2a792518d6f6be8a85f62fc73'
         'ce7933dc20de7e07427a6a6b5d4fd002')

build() {
  cd "$srcdir/$pkgname-$pkgver"
  patch -p1 -i "${srcdir}"/gcc47.patch

  #patch SConstruct so libs end up in /usr/lib not /usr/lib64 on X86_64
  sed -i -e "/LIBDIR_SCHEMA=/s/lib64/lib/" SConstruct
  sed -i 's|png_ptr->io_ptr|png_get_io_ptr(png_ptr)|g' src/png_reader.cpp
  sed -i 's/-ansi -Wall/-ansi -DBOOST_FILESYSTEM_VERSION=2 -Wall/' SConstruct

  scons configure \
    PREFIX="/usr" \
    INPUT_PLUGINS=all \
    DESTDIR="$pkgdir"
  scons
}

package(){
  cd "$srcdir/$pkgname-$pkgver"
  scons install
  # fix permissions on SCons-autogenerated files
  chmod 644 "${pkgdir}/usr/lib/python2.7/site-packages/mapnik/paths.py"
}
