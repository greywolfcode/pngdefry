cmake_minimum_required(VERSION 3.23)

project(pngdefry)

option(BUILD_AS_LIBRARY "Build pngdefry as shared library not executable" OFF)

include(GenerateExportHeader)

if(BUILD_AS_LIBRARY) 
    add_library(pngdefry SHARED)
    set_target_properties(pngdefry PROPERTIES C_VISIBILITY_PRESET hidden VISIBILITY_INLINES_HIDDEN 1)
    generate_export_header(pngdefry BASE_NAME pngdefry)
    target_include_directories(pngdefry PUBLIC ${CMAKE_CURRENT_BINARY_DIR})
    target_sources(pngdefry PRIVATE source/pngdefry.c "${CMAKE_CURRENT_BINARY_DIR}/pngdefry_export.h")
    set_source_files_properties("${CMAKE_CURRENT_BINARY_DIR}/pngdefry_export.h" PROPERTIES GENERATED TRUE)
else()
    add_executable(pngdefry)
    target_compile_definitions(pngdefry PRIVATE MYLIB_NO_EXPORT_LOGIC)
    target_sources(pngdefry PRIVATE source/pngdefry.c)
endif() 
