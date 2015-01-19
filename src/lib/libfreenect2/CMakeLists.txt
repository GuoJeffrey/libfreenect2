remake_project_header(config.h.remake INSTALL)

remake_set(LIBFREENECT2_RESOURCES
  bin/11to16.bin
  bin/xTable.bin
  bin/zTable.bin
  shader/debug.fs
  shader/default.vs
  shader/filter1.fs
  shader/filter2.fs
  shader/stage1.fs
  shader/stage2.fs
  cl/opencl_depth_packet_processor.cl
)
generate_resources(
  ${CMAKE_CURRENT_BINARY_DIR}/resources.inc
  ${CMAKE_SOURCE_DIR}/res
  ${LIBFREENECT2_RESOURCES}
)
remake_define(RESOURCES_INC ON)

remake_add_library(
  freenect2 PREFIX OFF
  *.cpp ${LIBFREENECT2_THREADING_SOURCE}
  GENERATED ${CMAKE_CURRENT_BINARY_DIR}/resources.inc
  LINK ${LIBUSB_1_0_LIBRARIES} ${OPENCL_LIBRARIES} ${GLFW3_LIBRARIES}
    ${GLEWMX_LIBRARIES} ${OPENCV_LIBRARIES} ${LIBTURBOJPEG_SO_0_LIBRARY}
)
remake_add_headers(*.h *.hpp RECURSE)

remake_pkg_config_generate()
