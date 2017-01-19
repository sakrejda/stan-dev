
## Provide GoogleTest 

ExternalProject_Add(boost
  GIT_REPOSITORY    https://github.com/google/googletest.git
  GIT_TAG           master
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/googletest-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/googletest-build"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     ""
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
)

# Specify include dir
ExternalProject_Get_Property(googletest GTEST_SOURCE_DIR)
set(GTEST_INCLUDE_DIR ${GTEST_SOURCE_DIR}/include)
ExternalProject_Get_Property(googletest GTEST_BINARY_DIR)
set(GTEST_LIBRARY gtest)
add_library(${GTEST_LIBRARY} UNKNOWN IMPORTED)
add_dependencies(${GTEST_LIBRARY} googletest)
add_library(${GTEST_LIBRARY}_main UNKNOWN IMPORTED)
add_dependencies(${GTEST_LIBRARY}_main googletest)
set_target_properties(gtest PROPERTIES
  IMPORTED_LOCATION ${GTEST_BINARY_DIR}/libgtest.a
)
set_target_properties(gtest_main PROPERTIES
  IMPORTED_LOCATION ${GTEST_BINARY_DIR}/libgtest_main.a
)

#include_directories(${GTEST_INCLUDE} ${GTEST_BASE})
#set(GTEST_ROOT ${GTEST_BASE})
#set(GTEST_INCLUDE_DIR ${GTEST_INCLUDE})
#set(GTEST_LIBRARY ${GTEST_BASE}/libgtest.a)
#set(GTEST_MAIN_LIBRARY ${GTEST_BASE}/libgtest-main.s)

