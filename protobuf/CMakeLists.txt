
## Provide Google Protobuf

ExternalProject_Add(protobuf
  GIT_REPOSITORY    https://github.com/google/protobuf.git
  GIT_TAG           master
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/protobuf-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/protobuf-build"
  CONFIGURE_COMMAND "cmake"
  BUILD_COMMAND     "make"
  INSTALL_COMMAND   ""
  TEST_COMMAND      ""
)

# Specify include dir
ExternalProject_Get_Property(protobuf PROTO_SOURCE_DIR)
set(PROTO_INCLUDE_DIR ${PROTO_SOURCE_DIR}/include)
ExternalProject_Get_Property(protobuf PROTO_BINARY_DIR)
set(PROTO_LIBRARY protobuf)
add_library(${PROTO_LIBRARY} UNKNOWN IMPORTED)
add_dependencies(${PROTO_LIBRARY} protobuf)
set_target_properties(protobuf PROPERTIES
  IMPORTED_LOCATION ${PROTO_BINARY_DIR}/libprotobuf.a
)

#include_directories(${PROTO_INCLUDE} ${PROTO_BASE})
#set(PROTO_ROOT ${PROTO_BASE})
#set(PROTO_INCLUDE_DIR ${PROTO_INCLUDE})
#set(PROTO_LIBRARY ${PROTO_BASE}/libprotobuf.a)

