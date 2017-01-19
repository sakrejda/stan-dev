
## Provide GoogleTest 

ExternalProject_Add(googletest
  GIT_REPOSITORY    https://github.com/google/googletest.git
  GIT_TAG           master
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/googletest-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/googletest-build"
  CONFIGURE_COMMAND "cmake"
  BUILD_COMMAND     "make"
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
)

# Dump variables to global environment:
ExternalProject_Get_Property(googletest GTEST_SOURCE_DIR)
ExternalProject_Get_Property(googletest GTEST_BINARY_DIR)

# GoogleTest include dir
set(GTEST_INCLUDE_DIR ${GTEST_SOURCE_DIR}/googletest/include)
include_directories(${GTEST_INCLUDE_DIR})
set(GTEST_ROOT ${GTEST_BINARY_DIR})
set(GTEST_LIBRARY ${GTEST_BINARY_DIR}/libgtest.a)
set(GTEST_MAIN_LIBRARY ${GTEST_BINARY_DIR}/libgtest-main.s)

