
download_project(
  PROJ              protostan
  GIT_REPOSITORY    https://github.com/sakrejda/protostan.git
  GIT_TAG           simplify
  SOURCE_DIR        "${CMAKE_BINARY_DIR}/protostan-src"
  BINARY_DIR        "${CMAKE_BINARY_DIR}/protostan-build"
)

add_custom_target(protostan-prerequisites ALL DEPENDS
  boost gtest gtest_main stan-math stanc protobuf)

add_subdirectory(${protostan_SOURCE_DIR} ${protostan_BINARY_DIR})
set(PROTOBUF_LIB_DIR ${protostan_BINARY_DIR} PARENT_SCOPE)



