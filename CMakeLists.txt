cmake_minimum_required(VERSION 2.8.3)
project(g2o_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple()

include(ExternalProject)

file(MAKE_DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/g2o)

ExternalProject_Add(g2o_src
  GIT_REPOSITORY https://github.com/RainerKuemmerle/g2o.git
  GIT_TAG "master"
  UPDATE_COMMAND ""
  CONFIGURE_COMMAND cd ../g2o_src && mkdir build && cd build && cmake ../
    -DCMAKE_INSTALL_PREFIX=${CATKIN_DEVEL_PREFIX}
    -DBUILD_SHARED_LIBS=ON
  BUILD_COMMAND cd ../g2o_src && make -j8
  INSTALL_COMMAND cd ../g2o_src/lib/ && cp libg2o_core.so ${CATKIN_DEVEL_PREFIX}/lib/
)

cs_add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} g2o_src)
target_link_libraries(${PROJECT_NAME}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_core${CMAKE_SHARED_LIBRARY_SUFFIX})

cs_install()

install(DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/g2o
  DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
  PATTERN "*.h"
  PATTERN ".git" EXCLUDE
)

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/g2o
  CFG_EXTRAS g2o-extras.cmake)
