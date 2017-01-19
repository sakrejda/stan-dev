cmake_minimum_required (VERSION 3.5)
project (protostan VERSION 0.0.0.9000)
cmake_policy(SET CMP0048 OLD)
include(CTest)

# Add Stan math
include_directories(${STAN_MATH_SRC})

# Add Stan
include_directories(${STAN_SRC}/src)

# Include Boost
set(BOOST lib/stan/lib/stan_math/lib/boost_1.58.0)
include_directories(${BOOST})

# Find libraries:
find_library(LIB_PROTOBUF protobuf)
find_library(LIB_GTEST gtest ${PROJECT_BINARY_DIR}/googletest/googletest)
find_library(LIB_GTEST_MAIN gtest_main ${PROJECT_BINARY_DIR}/googletest/googletest)
find_library(LIB_STANC stanc ${PROJECT_BINARY_DIR}/stan)





