cmake_minimum_required(VERSION 3.20)
project(Snap7 VERSION 1.4.2 LANGUAGES C CXX)

option(BUILD_EXAMPLES "Build examples" OFF)
option(BUILD_SHARED_LIBS "Build Snap7 as shared library" ON)

add_subdirectory(src)
add_subdirectory(release)
if(BUILD_EXAMPLES)
    add_subdirectory(examples)
endif()
