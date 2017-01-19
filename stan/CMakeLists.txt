
ExternalProject_Add(stan
  GIT_REPOSITORY    https://github.com/stan-dev/stan.git
  GIT_TAG           develop
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/stan-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/stan-build"
  CONFIGURE_COMMAND ""
  BUILD_COMMAND     make -C ${CMAKE_BINARY_DIR}/stan-src bin/libstanc.a
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
  DEPENDS           boost googletest stan-math
)

# Dump variables to global environment:
ExternalProject_Get_Property(stan SOURCE_DIR)
ExternalProject_Get_Property(stan BINARY_DIR)

# Stan include dir
set(STAN_SRC ${STAN_SOURCE_DIR}/stan/src)
include_directories(${STAN_SRC})

# Stan library dir
set(LIB_STANC ${STAN_SOURCE_DIR}/lib/libstanc.a)

# Collect Stan grammar files for libstanc.a
#file(GLOB STAN_GRAMMAR 
#  ${STAN_SRC}/stan/lang/grammars/*_inst.cpp
#  ${STAN_SRC}/stan/lang/grammars/*_def.cpp
#  ${STAN_SRC}/stan/lang/*_inst.cpp
#  ${STAN_SRC}/stan/lang/*_def.cpp
#)
#add_library(stanc STATIC ${STAN_GRAMMAR})
#


