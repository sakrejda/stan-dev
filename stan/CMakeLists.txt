

message("Getting Stan!")
download_project(
  PROJ             stan
  GIT_REPOSITORY   https://github.com/stan-dev/stan.git
  GIT_TAG          develop
  ${UPDATE_DISCONNECTED_IF_AVAILABLE}
)
  
set(STAN_SOURCE_DIR ${stan_SOURCE_DIR})
set(STAN_BINARY_DIR ${stan_BINARY_DIR}) 

# Stan include dir
set(STAN_SRC ${STAN_SOURCE_DIR}/src)
include_directories(${STAN_SRC})
message("STAN_SRC: " ${STAN_SRC})

add_definitions(
 -DBOOST_RESULT_OF_USE_TR1
 -DBOOST_NO_DECLTYPE 
 -DBOOST_DISABLE_ASSERTS
 -DFUSION_MAX_VECTOR_SIZE=12 
 -DNO_FPRINTF_OUTPUT 
 -DGTEST_USE_OWN_TR1_TUPLE)

file(GLOB STAN_GRAMMAR 
  ${STAN_SRC}/stan/lang/grammars/*_inst.cpp
  ${STAN_SRC}/stan/lang/grammars/*_def.cpp
  ${STAN_SRC}/stan/lang/*_inst.cpp
  ${STAN_SRC}/stan/lang/*_def.cpp
)
include_directories(${BOOST_INCLUDE_DIR})
add_library(stanc STATIC ${STAN_GRAMMAR})
add_dependencies(stanc boost gtest gtest_main stan-math)

set(STAN_LIB_DIR ${PROJECT_BINARY_DIR}/stan PARENT_SCOPE)
set(STAN_INCLUDE_DIR ${STAN_SOURCE_DIR}/src PARENT_SCOPE)




