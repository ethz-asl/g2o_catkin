cmake_minimum_required(VERSION 2.8.3)
project(g2o_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/g2o)

ExternalProject_Add(g2o_src
  GIT_REPOSITORY https://github.com/ffurrer/g2o.git
  GIT_TAG fix/suitesparse_include
  PREFIX ${CMAKE_CURRENT_BINARY_DIR}/g2o
  CMAKE_ARGS -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX} -DCMAKE_BUILD_TYPE=Release
  -DBUILD_SHARED_LIBS=ON
)

ExternalProject_Get_Property(g2o_src install_dir)
include_directories(${install_dir}/include ${SUITESPARSE_INCLUDE_DIRS})

cs_add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} g2o_src)
target_link_libraries(${PROJECT_NAME} ${SUITESPARSE_LIBRARIES})
cs_install()

install(DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/g2o
  DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
  PATTERN "*.h"
  PATTERN ".git" EXCLUDE
)

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/
  CFG_EXTRAS g2o-extras.cmake)
