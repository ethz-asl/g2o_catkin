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
  INSTALL_COMMAND cd ../g2o_src/lib/ &&
    cp libg2o_calibration_odom_laser.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_cli.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_core.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_csparse_extension.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_ext_freeglut_minimal.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_hierarchical.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_incremental.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_interactive.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_interface.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_opengl_helper.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_parser.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_simulator.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_solver_cholmod.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_solver_csparse.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_solver_dense.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_solver_eigen.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_solver_pcg.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_solver_slam2d_linear.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_solver_structure_only.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_stuff.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_tutorial_slam2d.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_data.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_icp.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_sba.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_sclam2d.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_sim3.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_slam2d.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_slam2d_addons.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_slam3d.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cp libg2o_types_slam3d_addons.so ${CATKIN_DEVEL_PREFIX}/lib/ &&
    cd ../ && mkdir -p ${CATKIN_DEVEL_PREFIX}/include/g2o/core/ &&
    cp build/g2o/config.h ${CATKIN_DEVEL_PREFIX}/include/g2o/ &&
    cp -r g2o ${CATKIN_DEVEL_PREFIX}/include/


)

cs_add_library(${PROJECT_NAME} src/dependency_tracker.cc)
add_dependencies(${PROJECT_NAME} g2o_src)
target_link_libraries(${PROJECT_NAME}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_core${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_calibration_odom_laser${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_cli${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_core${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_csparse_extension${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_ext_freeglut_minimal${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_hierarchical${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_incremental${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_interactive${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_interface${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_opengl_helper${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_parser${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_simulator${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_solver_cholmod${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_solver_csparse${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_solver_dense${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_solver_eigen${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_solver_pcg${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_solver_slam2d_linear${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_solver_structure_only${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_stuff${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_tutorial_slam2d${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_data${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_icp${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_sba${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_sclam2d${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_sim3${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_slam2d_addons${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_slam2d${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_slam3d_addons${CMAKE_SHARED_LIBRARY_SUFFIX}
  ${CATKIN_DEVEL_PREFIX}/lib/libg2o_types_slam3d${CMAKE_SHARED_LIBRARY_SUFFIX}
  )

cs_install()

install(DIRECTORY ${CATKIN_DEVEL_PREFIX}/include/g2o
  DESTINATION ${CATKIN_GLOBAL_INCLUDE_DESTINATION}
  FILES_MATCHING PATTERN "*.hpp"
  PATTERN "*.h"
  PATTERN ".git" EXCLUDE
)

cs_export(INCLUDE_DIRS ${CATKIN_DEVEL_PREFIX}/include/g2o
  CFG_EXTRAS g2o-extras.cmake)
