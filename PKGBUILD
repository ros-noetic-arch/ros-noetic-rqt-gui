# Script generated with import_catkin_packages.py.
# For more information: https://github.com/bchretien/arch-ros-stacks.
pkgdesc="ROS - rqt_gui provides the main to start an instance of the ROS integrated graphical user interface provided by qt_gui."
url='https://wiki.ros.org/rqt_gui'

pkgname='ros-noetic-rqt-gui'
pkgver='0.5.2'
arch=('any')
pkgrel=2
license=('BSD')

ros_makedepends=(
	ros-noetic-qt-gui
	ros-noetic-catkin
)

makedepends=(
	'cmake'
	'ros-build-tools'
	${ros_makedepends[@]}
)

ros_depends=(
	ros-noetic-qt-gui
	ros-noetic-catkin
)

depends=(
	${ros_depends[@]}
)

_dir="rqt-${pkgver}/rqt_gui"
source=(
	python39.patch
	"${pkgname}-${pkgver}.tar.gz"::"https://github.com/ros-visualization/rqt/archive/${pkgver}.tar.gz"
)

sha256sums=(
	'2d5364633ed6d009355c45eab8ab6042b2d9d9ceaa9896f54db13f2045ef3ad1'
	'9913fb6da15f0ccb9d995f8ea3be935d36bd255379c8ae19c0005207883299eb'
)

prepare() {
    cd "rqt-$pkgver"
    patch --forward --strip=1 --input="${srcdir}/python39.patch"
}

build() {
	# Use ROS environment variables.
	source /usr/share/ros-build-tools/clear-ros-env.sh
	[ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

	# Create the build directory.
	[ -d ${srcdir}/build ] || mkdir ${srcdir}/build
	cd ${srcdir}/build

	# Build the project.
	cmake ${srcdir}/${_dir} \
		-DCATKIN_BUILD_BINARY_PACKAGE=ON \
		-DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
		-DPYTHON_EXECUTABLE=/usr/bin/python \
		-DSETUPTOOLS_DEB_LAYOUT=OFF
	make
}

package() {
	cd "${srcdir}/build"
	make DESTDIR="${pkgdir}/" install
}
