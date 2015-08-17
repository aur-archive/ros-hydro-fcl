
pkgdesc="ROS - FCL is a collision checking library."
url='http://www.ros.org/'

pkgname='ros-hydro-fcl'
pkgver='0.2.9'
_pkgver_patch=1
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-hydro-octomap
  ros-hydro-libccd
  ros-hydro-catkin)
makedepends=('cmake' 'git' 'ros-build-tools'
  ${ros_makedepends[@]}
  boost
  pkg-config)

ros_depends=(ros-hydro-octomap
  ros-hydro-libccd)
depends=(${ros_depends[@]}
  boost)

_tag=release/hydro/fcl/${pkgver}-${_pkgver_patch}
_dir=fcl
source=("${_dir}"::"git+https://github.com/ros-gbp/fcl-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
