cmake_minimum_required(VERSION 2.8)

project(liblua)

if (MSVC)
	add_definitions(-DLUA_LIB -DLUA_BUILD_AS_DLL)
	add_definitions(/W3 /wd"4996" /wd"4819" /wd"4091" /wd"4099" /wd"4800" /MP /Gm-)
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd")
else()
	set(CMAKE_CXX_FLAGS "-g -Wall")
endif(MSVC)

set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

include_directories(${PROJECT_SOURCE_DIR}/include)
include_directories(.)

file(GLOB_RECURSE SRC_FILES "${PROJECT_SOURCE_DIR}/src/*")

#add_library(lua STATIC ${SRC_FILES})

add_library(lua SHARED ${SRC_FILES})

if (CMAKE_SYSTEM_NAME STREQUAL "Linux")
    # Linux
	target_compile_options(lua PRIVATE "-DLUA_USE_MKSTEMP")
endif()
