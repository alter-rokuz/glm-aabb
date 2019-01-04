if(APPLE)
  cmake_minimum_required(VERSION 2.8.11 FATAL_ERROR)
else()
  cmake_minimum_required(VERSION 2.8.7 FATAL_ERROR)
endif()

project(glm_aabb_test)

enable_testing()

#-----------------------------------------------------------------------
# 3rd party
#-----------------------------------------------------------------------

include_directories(${GTEST_INCLUDE_DIRS})
include_directories(../3party/googletest/googletest/include)
include_directories(../3party/glm)

#-----------------------------------------------------------------------
# C++11
#-----------------------------------------------------------------------
if (UNIX)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
  if (APPLE)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -stdlib=libc++")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} -stdlib=libc++")
  endif ()
endif ()

#-----------------------------------------------------------------------
# Setup source
#-----------------------------------------------------------------------
# Setup spire test sources. Even though this is a batch renderer, this is
# a good test of concept.

file(GLOB Sources
  "*.cpp"
  "*.hpp"
  )

########################################################################
# Setup executable

if (UNIX)
  if (NOT APPLE)
    set(PTHREADS "-pthread")
  endif()
endif()

add_executable(${PROJECT_NAME} ${Sources})
target_link_libraries(${PROJECT_NAME}
  gtest
  ${PTHREADS})

add_test(AllTests ${PROJECT_NAME})
