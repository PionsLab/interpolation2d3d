cmake_minimum_required(VERSION 3.16)

project(interpolation2d3d LANGUAGES Fortran)

file(GLOB SRC
  "${CMAKE_CURRENT_SOURCE_DIR}/src/*.f90"
)

add_library(interpolation2d3d ${SRC})

set_target_properties(interpolation2d3d PROPERTIES
  Fortran_MODULE_DIRECTORY "${CMAKE_CURRENT_BINARY_DIR}/mod"
)

target_include_directories(interpolation2d3d PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_BINARY_DIR}/mod>
)

option(INTERPOLATION2D3D_BUILD_TESTS "Build tests for interpolation2d3d" ON)

if(PROJECT_IS_TOP_LEVEL AND INTERPOLATION2D3D_BUILD_TESTS AND BUILD_TESTING)
  include(CTest)
  enable_testing()
  add_subdirectory(test)
endif()