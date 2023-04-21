# Script generated with create_pkgbuild.py
# For more information: https://github.com/ros-noetic-arch/ros-build-tools-py3
pkgdesc="ROS - The libg2o library from http://openslam.org/g2o.html."
url='https://github.com/RainerKuemmerle/g2o'

pkgname='ros-noetic-libg2o'
pkgver='2020.5.3'
_pkgver_patch=1

arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=()
makedepends=('cmake' 'ros-build-tools'
	${ros_makedepends[@]}
	eigen
	boost
	mesa
	suitesparse
)

ros_depends=(ros-noetic-catkin)
depends=(${ros_depends[@]}
	eigen
	boost
	mesa
	suitesparse
)
    
# Tarball version (faster download)
_dir="libg2o-release-release-noetic-libg2o-${pkgver}-${_pkgver_patch}"
source=(
	"${pkgname}-${pkgver}-${_pkgver_patch}.tar.gz"::"https://github.com/ros-gbp/libg2o-release/archive/release/noetic/libg2o/${pkgver}-${_pkgver_patch}.tar.gz"
	fix-python-scripts.sh
)
sha256sums=(
	'115c41cdce39bc27adf6522557b97749db1624a0692316486a855689b345dcb4'
	'5528486d640d91136276edda2075aefc06f360e6297e556051bae57b9479aeda'
)

    build() {
        # Use ROS environment variables
        source /usr/share/ros-build-tools/clear-ros-env.sh
        [ -f /opt/ros/noetic/setup.bash ] && source /opt/ros/noetic/setup.bash

        # Create build directory
        [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
        cd ${srcdir}/build

        # Fix Python2/Python3 conflicts
        ${srcdir}/fix-python-scripts.sh -v 3 ${srcdir}/${_dir}

        # Build project
        cmake ${srcdir}/${_dir} \
                -DCMAKE_BUILD_TYPE=Release \
                -DCATKIN_ENABLE_TESTING=0 \
                -DCATKIN_BUILD_BINARY_PACKAGE=ON \
                -DCMAKE_INSTALL_PREFIX=/opt/ros/noetic \
                -DPYTHON_EXECUTABLE=/usr/bin/python3 \
                -DPYTHON_INCLUDE_DIR=/usr/include/python3.7m \
                -DPYTHON_LIBRARY=/usr/lib/libpython3.7m.so \
                -DPYTHON_BASENAME=.cpython-37m \
                -DSETUPTOOLS_DEB_LAYOUT=OFF
    make
    }

    package() {
    cd "${srcdir}/build"
    make DESTDIR="${pkgdir}/" install
    }
    
