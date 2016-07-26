cmake_minimum_required(VERSION 2.6.2)

project( googletest-distribution )
find_package(qibuild QUIET)
# Currently qi_create_gtest does not work if googletest is
# built as a static library (misses dependency to pthread).
# Build as dynamic library until this problem is solved.
if (${qibuild_FOUND})
  set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)
endif()

enable_testing()

option(BUILD_GTEST "Builds the googletest subproject" OFF)

#Note that googlemock target already builds googletest
option(BUILD_GMOCK "Builds the googlemock subproject" ON)

if(BUILD_GMOCK)
  add_subdirectory( googlemock )
elseif(BUILD_GTEST)
  add_subdirectory( googletest )
endif()
