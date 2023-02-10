# Contributor: Wouter van der Wal <me@wjtje.dev>
# Maintainer: Wouter van der Wal <me@wjtje.dev>
pkgname=libcamera-apps
pkgver=1.1.1
pkgrel=0
pkgdesc="This is a small suite of libcamera-based apps that aim to copy the functionality of the existing \"raspicam\" apps."
url="https://www.raspberrypi.com/documentation/computers/camera_software.html"
arch="armv7 armhf aarch64"
license="BSD-2-Clause"
depends="libcamera libjpeg-turbo libexif libpng tiff boost"
makedepends="cmake libcamera-dev libjpeg-turbo-dev libexif-dev libpng-dev tiff-dev boost-dev"
checkdepends=""
install=""
subpackages=""
source=""
builddir="$srcdir/$pkgname-$pkgver"

prepare() {
	git clone --depth 1 --branch "v$pkgver" https://github.com/raspberrypi/libcamera-apps.git $builddir
}

build() {
	mkdir build && cd build
	cmake .. -DCMAKE_INSTALL_PREFIX=/usr -DENABLE_DRM=1 -DENABLE_X11=0 -DENABLE_QT=0 -DENABLE_OPENCV=0 -DENABLE_TFLITE=0
	make
}

check() {
	:
}

package() {
	install -Dm644 license.txt "$pkgdir"/usr/share/licenses/$pkgname/license.txt
	cd build && make DESTDIR="$pkgdir" install
}
