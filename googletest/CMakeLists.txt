
## Provide GoogleTest 
message("Find Google Test?")
find_package(GTest 1.7.0)
if(GTest_FOUND)
  message("Using system Google Test!")
  add_custom_target(googletest ALL)
else(GTest_FOUND)
  message("Getting Google Test!")
  ExternalProject_Add(googletest
    GIT_REPOSITORY    https://github.com/google/googletest.git
    GIT_TAG           master
    SOURCE_DIR        "${CMAKE_BINARY_DIR}/googletest-src"
    BINARY_DIR        "${CMAKE_BINARY_DIR}/googletest-build"
    CONFIGURE_COMMAND cd ${CMAKE_BINARY_DIR}/googletest-build && cmake ${CMAKE_BINARY_DIR}/googletest-src
    BUILD_COMMAND     "make"
    INSTALL_COMMAND   ""
    TEST_COMMAND      ""
  )
  
  # Dump variables to global environment:
  ExternalProject_Get_Property(googletest SOURCE_DIR)
  ExternalProject_Get_Property(googletest BINARY_DIR)
  
  # GoogleTest include dir
  set(GTEST_INCLUDE_DIR ${GTEST_SOURCE_DIR}/googletest/include)
  include_directories(${GTEST_INCLUDE_DIR})
  set(GTEST_ROOT ${GTEST_BINARY_DIR})
  set(GTEST_LIBRARY ${GTEST_BINARY_DIR}/libgtest.a)
  set(GTEST_MAIN_LIBRARY ${GTEST_BINARY_DIR}/libgtest-main.s)
endif(GTest_FOUND)

