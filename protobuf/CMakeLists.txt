
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

# Dump variables to global environment
ExternalProject_Get_Property(protobuf PROTO_SOURCE_DIR)
ExternalProject_Get_Property(protobuf PROTO_BINARY_DIR)

# Protobuf include dir
set(PROTO_INCLUDE_DIR ${PROTO_SOURCE_DIR}/src)
set(PROTO_ROOT ${PROTO_SOURCE_DIR})
set(PROTO_LIBRARY ${PROTO_BINARY_DIR}/libprotobuf.a)

