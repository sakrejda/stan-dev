
ExternalProject_Add(stan
  GIT_REPOSITORY    https://github.com/stan-dev/stan.git
  GIT_TAG           develop
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/stan-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/stan-build"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     ""
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
  DEPENDS           boost gtest gtest_main stan-math
)

# Dump variables to global environment:
ExternalProject_Get_Property(stan SOURCE_DIR)
ExternalProject_Get_Property(stan BINARY_DIR)

# Stan include dir
set(STAN_SRC ${SOURCE_DIR}/src)
include_directories(${STAN_SRC})

add_definitions(
 -DBOOST_RESULT_OF_USE_TR1
 -DBOOST_NO_DECLTYPE 
 -DBOOST_DISABLE_ASSERTS
 -DFUSION_MAX_VECTOR_SIZE=12 
 -DNO_FPRINTF_OUTPUT 
 -DGTEST_USE_OWN_TR1_TUPLE)

message("BOOST_INCLUDE_DIR: " ${BOOST_INCLUDE_DIR})
file(GLOB STAN_GRAMMAR 
  ${STAN_SRC}/stan/lang/grammars/*_inst.cpp
  ${STAN_SRC}/stan/lang/grammars/*_def.cpp
  ${STAN_SRC}/stan/lang/*_inst.cpp
  ${STAN_SRC}/stan/lang/*_def.cpp
)
include_directories(${BOOST_INCLUDE_DIR})
add_library(stanc STATIC ${STAN_GRAMMAR})

set(STAN_LIB_DIR ${PROJECT_BINARY_DIR}/stan PARENT_SCOPE)
set(STAN_INCLUDE_DIR ${SOURCE_DIR}/src PARENT_SCOPE)




