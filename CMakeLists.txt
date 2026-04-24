cmake_minimum_required(VERSION 3.23)

project(pngdefry)

option(BUILD_AS_LIBRARY "Build pngdefry as shared library not executable" OFF)

if(BUILD_AS_LIBRARY)
add_library(pngdefry SHARED)
target_sources(pngdefry PUBLIC source/pngdefry.c)
else()
add_executable(pngdefry)
target_sources(pngdefry PRIVATE source/pngdefry.c)
endif()