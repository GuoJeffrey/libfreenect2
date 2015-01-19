cmake_minimum_required(VERSION 2.6)

include(ReMake)

remake_project(
  libfreenect2
  VERSION 0.1
  RELEASE beta
  SUMMARY "Driver library for the Kinect Version 2 (Xbox One) device."
  AUTHOR "Joshua Blake"
  AUTHOR "Florian Echtler"
  AUTHOR "Christian Kerl"
  CONTACT "joshblake@gmail.com"
  HOME "http://github.com/ethz-asl/libfreenect2"
  LICENSE "GNU General Public License Version 2 (GPL2)"
  README README.md
  INSTALL /usr
  PREFIX freenect2-
  EXTRA_CXX_FLAGS "-msse2 -std=c++0x"
)

remake_component(
  udev
  CONFIGURATION_DESTINATION /etc/udev
)
remake_add_directories(
  rules
  COMPONENT udev
)
remake_doc(
  html
)

remake_pack_deb(
  DEPENDS "libusb-1.0-0 (>= 2:1.0.19-2~)" ocl-icd-libopencl1 libglfw3
    libglewmx1.11 libopencv-core2.4 libturbojpeg
)
remake_pack_deb(
  COMPONENT utils
  DEPENDS libfreenect2 libboost-program-options[0-9.]*
  DESCRIPTION "utilities"
)
remake_pack_deb(
  COMPONENT dev
  DEPENDS libfreenect2 "libusb-1.0-0-dev (>= 2:1.0.19-2~)" libglfw3-dev
    "libglewmx-dev (>= 1.11.0)"
  DESCRIPTION "development headers"
)
remake_pack_deb(
  COMPONENT udev
  DESCRIPTION "udev rules"
  DEPENDS udev
  EXTRA debian/rules/*
)
remake_pack_deb(
  ARCH all
  COMPONENT doc
  DESCRIPTION "documentation"
)

remake_distribute_deb(
  DISTRIBUTION trusty
  SECTION libs
  UPLOAD ppa:kralf/asl
  DEPENDS "libusb-1.0-0-dev (>= 2:1.0.19-2~)" ocl-icd-libopencl1 opencl-headers
    libglfw3-dev "libglewmx-dev (>= 1.11.0)" libopencv-dev libturbojpeg
    libjpeg-turbo8-dev libboost-program-options-dev remake pkg-config doxygen
  PASS CMAKE_BUILD_TYPE LIBFREENECT2_GIT_REVISION
)
