# Contributor: Firas Zaidan <firas@zaidan.de>
pkgdesc="ROS - This package provides a recovery behavior for the navigation stack that attempts to clear space by reverting the costmaps used by the navigation stack to the static map outside of a given area."
url='http://wiki.ros.org/clear_costmap_recovery'

pkgname='ros-kinetic-clear-costmap-recovery'
pkgver='1.14.1'
_pkgver_patch=0
arch=('any')
pkgrel=1
license=('BSD')

ros_makedepends=(ros-kinetic-nav-core
  ros-kinetic-roscpp
  ros-kinetic-costmap-2d
  ros-kinetic-catkin
  ros-kinetic-cmake-modules
  ros-kinetic-tf
  ros-kinetic-pluginlib)
makedepends=('cmake' 'ros-build-tools'
  ${ros_makedepends[@]}
  eigen3)

ros_depends=(ros-kinetic-nav-core
  ros-kinetic-tf
  ros-kinetic-pluginlib
  ros-kinetic-roscpp
  ros-kinetic-costmap-2d)
depends=(${ros_depends[@]}
  eigen3)

# Git version (e.g. for debugging)
#_tag=release/kinetic/clear_costmap_recovery/${pkgver}-${_pkgver_patch}
#_dir=${pkgname}
#source=("${_dir}"::"git+https://github.com/ros-gbp/navigation-release.git"#tag=${_tag})
#sha256sums=('SKIP')

# Tarball version (faster download)
_dir="navigation-release-release-kinetic-clear_costmap_recovery-${pkgver}-${_pkgver_patch}"
 source=("${pkgname}-${pkgver}-${_pkgver_patch}.tar.gz"::"https://github.com/ros-gbp/navigation-release/archive/release/kinetic/clear_costmap_recovery/${pkgver}-${_pkgver_patch}.tar.gz")
 sha256sums=('aa9a4aad6055676116e1f3aad7f362c36fb3d2b52b57fa12e834208329bd57aa')

build() {
  # Use ROS environment variables
  source /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/kinetic/setup.bash ] && source /opt/ros/kinetic/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python2/Python3 conflicts
  /usr/share/ros-build-tools/fix-python-scripts.sh -v 2 ${srcdir}/${_dir}

  # Build project
  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/kinetic \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DPYTHON_BASENAME=-python2.7 \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
