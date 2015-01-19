remake_find_package(libusb-1.0 CONFIG)
remake_find_package(glfw3 CONFIG)
remake_find_package(glewmx CONFIG)
remake_find_package(opencv CONFIG)
remake_find_library(libturbojpeg.so.0 turbojpeg.h)
remake_find_package(
  Boost REQUIRED
  COMPONENTS program_options
  RESULT_VAR Boost_FOUND
)

remake_set(LIBFREENECT2_WITH_OPENCL_SUPPORT 1)
remake_define(GLEW_MX ON)

remake_include(
  lib
  ${LIBUSB_1_0_INCLUDE_DIRS}
  ${OPENCL_INCLUDE_DIRS}
  ${GLFW3_INCLUDE_DIRS}
  ${GLEWMX_INCLUDE_DIRS}
  ${OPENCV_INCLUDE_DIRS}
  ${LIBTURBOJPEG_SO_0_HEADERS}
  ${Boost_INCLUDE_DIRS}
)

remake_add_directories(lib bin)
