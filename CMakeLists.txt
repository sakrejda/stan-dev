cmake_minimum_required (VERSION 3.5)
project (protostan VERSION 0.0.0.9000)
cmake_policy(SET CMP0048 OLD)
include(CTest)
include(ExternalProject)

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




