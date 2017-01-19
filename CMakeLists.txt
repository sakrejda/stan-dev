cmake_minimum_required (VERSION 3.5)
project (protostan VERSION 0.0.0.9000)
cmake_policy(SET CMP0048 OLD)
include(CTest)
include(ExternalProject)

set(UPDATE_DISCONNECTED_IF_AVAILABLE "UPDATE_DISCONNECTED 1")
include(DownloadProject.cmake)

# Boost
add_subdirectory(boost)

# Google test framework
add_subdirectory(googletest)

# Google protobuf framework
add_subdirectory(protobuf)

# Stan math library
message("Getting Stan math library.")
add_subdirectory(stan-math)

# Stan algorithms and language compiler
message("Getting Stan language and algorithms.")
add_subdirectory(stan)

# Getting to the goods.
message("Getting Stan protobuf interface.")
add_subdirectory(protostan)



download_project(PROJ                googletest
                 GIT_REPOSITORY      https://github.com/google/googletest.git
                 GIT_TAG             master
                 ${UPDATE_DISCONNECTED_IF_AVAILABLE}
)

# Prevent GoogleTest from overriding our compiler/linker options
# when building with Visual Studio
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR})

# When using CMake 2.8.11 or later, header path dependencies
# are automatically added to the gtest and gmock targets.
# For earlier CMake versions, we have to explicitly add the
# required directories to the header search path ourselves.
if (CMAKE_VERSION VERSION_LESS 2.8.11)
    include_directories("${gtest_SOURCE_DIR}/include"
                        "${gmock_SOURCE_DIR}/include")
endif()

# Trivial example using gtest and gmock
add_executable(example example.cpp)
target_link_libraries(example gtest gmock_main)
add_test(NAME example_test COMMAND example)
