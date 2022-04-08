cmake_minimum_required(VERSION 3.10)

# Determine if ntcl is built as a subproject (using add_subdirectory)
# or if it is the main project.
if(NOT DEFINED NTCL_MAIN_PROJECT)
  set(NTCL_MAIN_PROJECT OFF)
  if(CMAKE_CURRENT_SOURCE_DIR STREQUAL CMAKE_SOURCE_DIR)
    set(NTCL_MAIN_PROJECT ON)
  endif()
endif()

# Set the default CMAKE_BUILD_TYPE to Release.
# This should be done before the project command since the latter can set
# CMAKE_BUILD_TYPE itself (it does so for nmake).
if(NTCL_MAIN_PROJECT AND NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Release)
endif()

project(
    ntcl
    VERSION
    0.1.0
)

enable_language(Fortran)

if(NTCL_MAIN_PROJECT)
  add_compile_options("-Wall" "-Wextra" "-std=f2008ts" "$<$<CONFIG:RELEASE>:-O3>")
endif()

set(NTCL_ROOT_DIR ${CMAKE_CURRENT_SOURCE_DIR})
set(NTCL_BUILD_DIR ${CMAKE_CURRENT_BINARY_DIR})

add_subdirectory(ntcl-util)
add_subdirectory(ntcl-data)
add_subdirectory(ntcl-tensor)
