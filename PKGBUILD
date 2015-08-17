# Maintainer: Christian Hesse <mail@eworm.de>

pkgname=opera-stable
pkgver=26.0.1656.32
pkgrel=1
pkgdesc='A fast and secure web browser and Internet suite - beta stream'
arch=('x86_64')
url='http://www.opera.com/browser/'
license=('custom:opera')
depends=('alsa-lib' 'nss' 'gtk2' 'gconf' 'libxss' 'libxtst' 'desktop-file-utils')
optdepends=('ffmpeg: HTML5 H264 and mp3 playback')
conflicts=('opera')
install=opera.install
options=(!strip)

if [[ "${CARCH}" == 'i686' ]]; then
	# no i686 at this time!
	_arch='i386'
	source=()
	sha256sums=()
elif [[ "${CARCH}" == 'x86_64' ]]; then
	_arch="${CARCH}"
	source=("http://get.geo.opera.com/pub/opera/desktop/${pkgver}/linux/${pkgname}_${pkgver}_amd64.deb")
	sha256sums=('e2ea368709f2ac10c3997dd361440cb39b4735b6dfe77e29a271e27f6df78a6a')
fi

prepare() {
	cd ${srcdir}/

	# extract the tarball
	tar xJf data.tar.xz

	# fix opera to use libudev.so.1 and libav*.so from ffmpeg 2.4.x
	sed -i -e 's/libudev.so.0/libudev.so.1/g' \
		-e 's/libavcodec.so.55/libavcodec.so.56/g' \
		-e 's/libavformat.so.55/libavformat.so.56/g' \
		-e 's/libavutil.so.52/libavutil.so.54/g' \
		usr/lib/x86_64-linux-gnu/opera/opera
}

package() {
	cd ${srcdir}/

	# copy to pkgdir
	cp -a usr/ "${pkgdir}/"

	# set suid bit for Opera sandbox
	chmod 4755 "${pkgdir}/usr/lib/x86_64-linux-gnu/opera/opera_sandbox"
}

