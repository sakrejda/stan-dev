
ExternalProject_Add(stan
  GIT_REPOSITORY    https://github.com/stan-dev/stan.git
  GIT_TAG           develop
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/stan-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/stan-build"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     "make"
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
)

# Stan include dir
set(STAN_SRC ${STAN_SOURCE_DIR}/src)
include_directories(${STAN_SRC})

# Collect Stan grammar files for libstanc.a
file(GLOB STAN_GRAMMAR 
  ${STAN_SRC}/stan/lang/grammars/*_inst.cpp
  ${STAN_SRC}/stan/lang/grammars/*_def.cpp
  ${STAN_SRC}/stan/lang/*_inst.cpp
  ${STAN_SRC}/stan/lang/*_def.cpp
)
add_library(stanc STATIC ${STAN_GRAMMAR})

# Dump variables to global environment:
ExternalProject_Get_Property(stan STAN_SOURCE_DIR)
ExternalProject_Get_Property(stan STAN_BINARY_DIR)

# Add project product as dependent
set(STAN_LIBRARY stanc)
add_library(${STAN_LIBRARY} UNKNOWN IMPORTED)
add_dependencies(${STAN_LIBRARY} stan)
set_target_properties(stan PROPERTIES
  IMPORTED_LOCATION ${STAN_BINARY_DIR}/libstanc.a
)


