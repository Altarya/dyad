#Initial setup
cmake_minimum_required(VERSION 3.0.0)
project(dyad VERSION 0.1.0)

set(BUILD_DEBUG OFF) #Change to true when debugging
if(CMAKE_BUILD_TYPE STREQUAL "Debug")
	message("Building debug!")
	set(BUILD_DEBUG ON)
endif(CMAKE_BUILD_TYPE STREQUAL "Debug")

option(BUILD_DYAD_STATIC "Build Dyad as a static library" OFF)

#Setup target
file(GLOB dyad_headers ${CMAKE_SOURCE_DIR}/src/*.h)
file(GLOB dyad_sources ${CMAKE_SOURCE_DIR}/src/*.c)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src)
if(BUILD_STATIC)
    add_library(dyad STATIC ${dyad_sources} ${dyad_headers})
    else()
    add_library(dyad SHARED ${dyad_sources} ${dyad_headers})
endif(BUILD_STATIC)

if(WIN32)
    target_link_libraries(dyad PRIVATE wsock32 ws2_32)
endif(WIN32)

#Use C17
set_property(TARGET dyad PROPERTY C_STANDARD 17)
set_property(TARGET dyad PROPERTY C_STANDARD_REQUIRED ON)
