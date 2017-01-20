
## Provide Google Protobuf
message("Find Protobuf?")
find_package(Protobuf)
if(Protobuf_FOUND)
  message("Using system Protobuf!")
  add_custom_target(protobuf)
else(Protobuf_FOUND)
  message("Getting Protobuf!")
  download_project(
    PROJ protobuf
    GIT_REPOSITORY    https://github.com/google/protobuf.git
    GIT_TAG           master
    ${UPDATE_DISCONNECTED_IF_AVAILABLE}
  )
  add_subdirectory(${protobuf_SOURCE_DIR} ${protobuf_BINARY_DIR})
  set(PROTOBUF_LIB_DIR ${protobuf_BINARY_DIR} PARENT_SCOPE)
endif(Protobuf_FOUND)


