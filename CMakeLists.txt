cmake_minimum_required(VERSION 2.8.0 FATAL_ERROR)
project(glm_aabb)

set(SOURCE_LIB glm-aabb/AABB.hpp)

OPTION(GLM_AABB_BUILD_TESTS "If the test suite is built in addition to the library." OFF)

if (GLM_AABB_BUILD_TESTS)
  add_subdirectory(3party/googletest)
  add_subdirectory(tests)
endif()
