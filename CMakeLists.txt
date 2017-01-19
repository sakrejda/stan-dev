cmake_minimum_required (VERSION 3.5)
project (protostan VERSION 0.0.0.9000)
cmake_policy(SET CMP0048 OLD)
include(CTest)
include(ExternalProject)

# Boost
message("Find Boost?")
find_package(Boost 1.58.0)
if(Boost_FOUND)
  message("Using system Boost!")
  include_directories(${Boost_INCLUDE_DIRS})
else(Boost_FOUND)
  message("Getting Boost!")
  add_subdirectory(boost)
endif(Boost_FOUND)

# Google test framework
message("Find Google Test?")
find_package(GTest 1.7.0)
if(GTest_FOUND)
  message("Using system Google Test!")
else(GTest_FOUND)
  message("Getting Google Test!")
  add_subdirectory(googletest)
endif(GTest_FOUND)

# Google protobuf framework
message("Find Protobuf?")
find_package(Protobuf)
if(Protobuf_FOUND)
  message("Using system Protobuf!")
else(Protobuf_FOUND)
  message("Getting Protobuf!")
  add_subdirectory(protobuf)
endif(Protobuf_FOUND)

# Stan math library
message("Getting Stan math library.")
add_subdirectory(stan-math)

# Stan algorithms and language compiler
message("Getting Stan language and algorithms.")
add_subdirectory(stan)

# Getting to the goods.
message("Getting Stan protobuf interface.")
add_subdirectory(proto)




