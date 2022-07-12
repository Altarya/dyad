#Initial setup
cmake_minimum_required(VERSION 3.0.0)
project(dyad VERSION 0.1.0)

set(BUILD_DEBUG OFF) #Change to true when debugging
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
	message("Building debug!")
	set(BUILD_DEBUG ON)
endif(CMAKE_BUILD_TYPE STREQUAL "Debug")

set(DYAD_DIR "${CMAKE_CURRENT_SOURCE_DIR}/")
include_directories("${DYAD_DIR}/src")
add_library(dyad STATIC "${DYAD_DIR}/src/dyad.c" "${DYAD_DIR}/src/dyad.h")
