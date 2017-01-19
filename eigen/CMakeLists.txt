
ExternalProject_Add(eigen
  HG_REPOSITORY    https://bitbucket.org/eigen/eigen/
  HG_TAG           develop
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/eigen-src"
  BINARY_DIR        ""
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     ""
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
)

# Stan include dir
set(EIGEN_SRC ${EIGEN_SOURCE_DIR}/src)
include_directories(${EIGEN_SRC})




