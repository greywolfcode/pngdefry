cmake_minimum_required(VERSION 3.23)

project(pngdefry)

option(BUILD_AS_LIBRARY "Build pngdefry as shared library not executable" OFF)

include(GenerateExportHeader)


if(BUILD_AS_LIBRARY) 
    add_library(pngdefry SHARED)
    set_target_properties(pngdefry PROPERTIES C_VISIBILITY_PRESET hidden VISIBILITY_INLINES_HIDDEN 1)
    target_sources(pngdefry PUBLIC source/pngdefry.c)
    generate_export_header(pngdefry)
else()
    add_executable(pngdefry)
    target_sources(pngdefry PRIVATE source/pngdefry.c)
    target_compile_definitions(pngdefry PRIVATE MYLIB_NO_EXPORT_LOGIC)
    generate_export_header(pngdefry STATIC_DEFINE MYLIB_NO_EXPORT_LOGIC)
endif() 

target_include_directories(pngdefry PUBLIC ${CMAKE_CURRENT_BINARY_DIR})