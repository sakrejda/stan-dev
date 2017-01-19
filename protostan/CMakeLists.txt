
ExternalProject_Add(protostan
  GIT_REPOSITORY    https://github.com/sakrejda/protostan.git
  GIT_TAG           develop
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/protostan-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/protostan-build"
  CONFIGURE_COMMAND cd ${CMAKE_BINARY_DIR}/protostan-build && cmake ${CMAKE_BINARY_DIR}/protostan-src
  BUILD_COMMAND     "make"
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
  DEPENDS           boost googletest stan stan-math
)


# Add Stan math
include_directories(${STAN_MATH_SRC})

# Add Stan
include_directories(${STAN_SRC}/src)

# Include Boost
set(BOOST lib/stan/lib/stan_math/lib/boost_1.58.0)
include_directories(${BOOST})





