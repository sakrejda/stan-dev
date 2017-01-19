
ExternalProject_Add(stan-math
  GIT_REPOSITORY    https://github.com/stan-dev/math.git
  GIT_TAG           develop
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/stan-math-src"
  BINARY_DIR        ""
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     ""
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
)

# Stan include dir
set(STAN_MATH_SRC ${STAN_MATH_SOURCE_DIR}/src)
include_directories(${STAN_MATH_SRC})




