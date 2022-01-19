# This is an example PKGBUILD file. Use this as a start to creating your own,
# and remove these comments. For more information, see 'man PKGBUILD'.
# NOTE: Please fill out the license field for your package! If it is unknown,
# then please put 'unknown'.

# Maintainer: bobosito <bobosito000@gmail.com>
pkgname=qgroundcontrol-git
pkgver=v4.2.0.r37.1d0917c44
pkgrel=1
epoch=
# extract_name=wjakob-tbb-9e219e2
pkgdesc="ground control system for px4 autopilot"
arch=('any')
url=""
license=('GPL')
groups=()
depends=()
makedepends=('git')
checkdepends=()
optdepends=()
provides=("${pkgname%-git}")
conflicts=("${pkgname%-git}")
replaces=()
backup=()
options=()
install=
changelog=
source=("qgroundcontrol::git+https://github.com/mavlink/qgroundcontrol.git#branch=master")
sha256sums=('SKIP')
# noextract=("v2020.3.tar.gz")
md5sums=()
validpgpkeys=()

pkgver() {
	cd "$srcdir/${pkgname%-git}"
	# Git, tags available
	printf "%s" "$(git describe --long | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}


prepare() {
	cd $srcdir/${pkgname%-git}
	git submodule update --init --recursive
	# git apply $srcdir/patch
	echo $PWD
	patch -p1 -i "$srcdir/patch"
	cmake . -B ./build \
		-DCMAKE_BUILD_TYPE=Release \
		-DCMAKE_INSTALL_PREFIX=/usr
}

build() {
	cd $srcdir/${pkgname%-git}
	cmake --build ./build
}
# check() {
# 	cd build
# 	# ctest --output-on-failure
# }

package() {
	cd $srcdir/${pkgname%-git}/build
	make DESTDIR=$pkgdir install
}
