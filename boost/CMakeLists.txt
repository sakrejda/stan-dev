
## Provide Boost
message("Find Boost?")
find_package(Boost 1.58.0)
if(Boost_FOUND)
  message("Using system Boost!")
  add_custom_target(boost ALL)
  # GoogleTest include dir
  include_directories(${Boost_INCLUDE_DIRS})
else(Boost_FOUND)
  message("Getting Boost!")
  ExternalProject_Add(boost
    GIT_REPOSITORY    https://github.com/boostorg/boost.git
    GIT_TAG           develop
    SOURCE_DIR        "${CMAKE_BINARY_DIR}/boost-src"
    BINARY_DIR        "${CMAKE_BINARY_DIR}/boost-build"
    CONFIGURE_COMMAND ""
    BUILD_COMMAND     ""
    INSTALL_COMMAND   ""
    TEST_COMMAND      ""
  )
  
  # Dump variables to global environment:
  ExternalProject_Get_Property(boost BOOST_SOURCE_DIR)
  ExternalProject_Get_Property(boost BOOST_BINARY_DIR)
  
  # GoogleTest include dir
  set(BOOST_INCLUDE_DIR ${BOOST_SOURCE_DIR}/boost/include)
  include_directories(${BOOST_INCLUDE_DIR})
endif(Boost_FOUND)


