
## Provide GoogleTest 
message("Find Google Test?")
find_package(GTest 1.7.0)
if(GTest_FOUND)
  message("Using system Google Test!")
  add_custom_target(googletest ALL)
  add_custom_target(gtest ALL)
  add_custom_target(gtest_main ALL)
else(GTest_FOUND)
  message("Getting Google Test!")
  download_project(PROJ                googletest
                   GIT_REPOSITORY      https://github.com/google/googletest.git
                   GIT_TAG             master
                   ${UPDATE_DISCONNECTED_IF_AVAILABLE}
  )
  
  # Prevent GoogleTest from overriding our compiler/linker options
  # when building with Visual Studio
  set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

  add_subdirectory(${googletest_SOURCE_DIR} ${googletest_BINARY_DIR}) 

  set(GTEST_SOURCE_DIR ${CMAKE_BINARY_DIR}/googletest-src)
  set(GTEST_BINARY_DIR ${CMAKE_BINARY_DIR}/googletest-build)
  #add_subdirectory(${GTEST_SOURCE_DIR} ${GTEST_BINARY_DIR})
  message("GTEST_SOURCE_DIR: " ${GTEST_SOURCE_DIR})
  message("GTEST_BINARY_DIR: " ${GTEST_BINARY_DIR})

  set(GTEST_LIB_DIR ${GTEST_BINARY_DIR}/googlemock/gtest PARENT_SCOPE)
  set(GTEST_LIBRARY ${GTEST_BINARY_DIR}/googlemock/gtest/libgtest.a PARENT_SCOPE)
  set(GTEST_MAIN_LIBRARY ${GTEST_BINARY_DIR}/googlemock/gtest/libtest_main.a PARENT_SCOPE)
  set(GTEST_INCLUDE_DIR ${GTEST_SOURCE_DIR}/googletest/include PARENT_SCOPE)
endif(GTest_FOUND)


