cmake_minimum_required(VERSION 2.8.12)
project(cmake_wrapper)

if(EXISTS "${CMAKE_BINARY_DIR}/conanbuildinfo.cmake")
  include("${CMAKE_BINARY_DIR}/conanbuildinfo.cmake")
else()
  include(conanbuildinfo.cmake)
endif()
conan_basic_setup()

if (MINGW)
    add_compile_options(-Wno-unknown-pragmas -Wno-format -Wno-cpp)
endif()

if((CMAKE_COMPILER_IS_GNUCC OR CMAKE_COMPILER_IS_GNUCXX) AND
   (CMAKE_CXX_COMPILER_VERSION VERSION_EQUAL "9.0" OR CMAKE_CXX_COMPILER_VERSION VERSION_GREATER "9.0"))
       add_compile_options(-Wno-deprecated-copy)
endif()

add_subdirectory("source_subfolder")
