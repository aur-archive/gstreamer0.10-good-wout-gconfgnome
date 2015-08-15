# Baed on: Jan de Groot <jgc@archlinux.org>
# Mod: Gustavo Alvarez <sl1pkn07@gmail.com>

pkgname=gstreamer0.10-good-wout-gconfgnome
true && pkgname=('gstreamer0.10-good-wout-gconfgnome' 'gstreamer0.10-good-plugins-good-wout-gconfgnome')
pkgdesc="GStreamer Multimedia Framework Good plugin libraries (Without Gconf & Gnome)"
pkgver=0.10.31
pkgrel=2
arch=('i686' 'x86_64')
license=('LGPL')
makedepends=('intltool' 'pkgconfig' 'gstreamer0.10-base>=0.10.34' 'libavc1394' 'libiec61883' 'aalib' 'libshout' 'libdv' 'flac' 'wavpack' 'taglib' 'v4l-utils' 'libcaca' 'bzip2' 'gdk-pixbuf2' 'libpulse' 'jack' 'udev')
url="http://gstreamer.freedesktop.org/"
options=(!libtool !emptydirs)
source=("${url}/src/gst-plugins-good/gst-plugins-good-${pkgver}.tar.bz2")
sha256sums=('7e27840e40a7932ef2dc032d7201f9f41afcaf0b437daf5d1d44dc96d9e35ac6')

build() {
  cd "${srcdir}/gst-plugins-good-${pkgver}"
  sed -i '/AC_PATH_XTRA/d' configure.ac
  autoreconf
  ./configure --prefix=/usr --sysconfdir=/etc --localstatedir=/var \
    --disable-static --enable-experimental \
    --disable-schemas-install \
    --disable-gconftool \
    --disable-gconf \
    --disable-hal \
    --disable-esd \
    --disable-soup \
    --disable-gst_v4l2 \
    --with-package-name="GStreamer Good Plugins (Archlinux)" \
    --with-package-origin="http://www.archlinux.org/"

  make
  sed -e 's/gst sys ext/gst/' -i Makefile
}

package_gstreamer0.10-good-wout-gconfgnome(){
  depends=('gstreamer0.10-base' 'bzip2')
  pkgdesc="GStreamer Multimedia Framework Good plugin libraries"
  preplaces=('gstreamer0.10-good')
  provides=('gstreamer0.10-good')

  cd "${srcdir}/gst-plugins-good-${pkgver}"
  make GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="${pkgdir}" install
  rm -rf "${pkgdir}/etc/gconf"
}

package_gstreamer0.10-good-plugins-good-wout-gconfgnome() {
  depends=('gstreamer0.10-good-wout-gconfgnome' 'libavc1394' 'libiec61883' 'aalib' 'libshout' 'libdv' 'flac' 'wavpack' 'taglib' 'libcaca' 'libpng' 'libjpeg' 'jack' 'libpulse' 'gdk-pixbuf2' 'cairo' 'jack' 'udev')
  pkgdesc="GStreamer Multimedia Framework Good Plugins (gst-plugins-good)"
  replaces=('gstreamer0.10-aalib' 'gstreamer0.10-wavpack' 'gstreamer0.10-shout2' 'gstreamer0.10-taglib' 'gstreamer0.10-libcaca' 'gstreamer0.10-libpng' 'gstreamer0.10-jpeg' 'gstreamer0.10-cairo' 'gstreamer0.10-flac' 'gstreamer0.10-speex' 'gstreamer0.10-gdkpixbuf' 'gstreamer0.10-dv1394' 'gstreamer0.10-annodex' 'gstreamer0.10-gconf' 'gstreamer0.10-esd' 'gstreamer0.10-cdio' 'gstreamer0.10-dv' 'gstreamer0.10-soup' 'gstreamer0.10-pulse' 'gstreamer0.10-good-plugins')
  conflicts=('gstreamer0.10-aalib' 'gstreamer0.10-wavpack' 'gstreamer0.10-shout2' 'gstreamer0.10-taglib' 'gstreamer0.10-libcaca' 'gstreamer0.10-libpng' 'gstreamer0.10-jpeg' 'gstreamer0.10-cairo' 'gstreamer0.10-flac' 'gstreamer0.10-speex' 'gstreamer0.10-gdkpixbuf' 'gstreamer0.10-dv1394' 'gstreamer0.10-annodex' 'gstreamer0.10-gconf' 'gstreamer0.10-esd' 'gstreamer0.10-cdio' 'gstreamer0.10-dv' 'gstreamer0.10-soup' 'gstreamer0.10-pulse' 'gstreamer0.10-bad-plugins<0.10.7')
  provides=('gstreamer0.10-good-plugins')

  cd "${srcdir}/gst-plugins-good-${pkgver}"
  make -C sys DESTDIR="${pkgdir}" install
  make -C ext GCONF_DISABLE_MAKEFILE_SCHEMA_INSTALL=1 DESTDIR="${pkgdir}" install
}
