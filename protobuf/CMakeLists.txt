
## Provide Google Protobuf
message("Find Protobuf?")
find_package(Protobuf)
if(Protobuf_FOUND)
  message("Using system Protobuf!")
  add_custom_target(protobuf)
  set(PROTOBUF_LIBS ${Protobuf_LIBRARIES} PARENT_SCOPE)
  set(PROTOBUF_INCLUDE_DIR ${Protobuf_INCLUDE_DIRS} PARENT_SCOPE)
else(Protobuf_FOUND)
  message("Getting Protobuf!")
  download_project(
    PROJ protobuf
    GIT_REPOSITORY    https://github.com/google/protobuf.git
    GIT_TAG           master
    ${UPDATE_DISCONNECTED_IF_AVAILABLE}
  )
  add_subdirectory(${protobuf_SOURCE_DIR} ${protobuf_BINARY_DIR})
  set(PROTOBUF_LIBS ${protobuf_BINARY_DIR}/libprotobuf.a PARENT_SCOPE)
  set(PROTOBUF_INCLUDE_DIR ${protobuf_SOURCE_DIR}/src/google/protobuf)
endif(Protobuf_FOUND)


