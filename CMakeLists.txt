cmake_minimum_required(VERSION 2.8)
project(dlib_colcon)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_CURRENT_LIST_DIR}/cmake")

include(ExternalProject)
externalproject_add(dlib_src
  GIT_REPOSITORY https://github.com/davisking/dlib.git
  GIT_TAG 3162f93c5d303e593337ab8e40d79b385e025d3c
  CONFIGURE_COMMAND cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX} -DDLIB_USE_CUDA=OFF ../dlib_src
  BUILD_COMMAND make
  INSTALL_COMMAND make install
)

install(DIRECTORY include/${PROJECT_NAME}/
  DESTINATION "include/${PROJECT_NAME}"
  FILES_MATCHING PATTERN "*.h"
)

install(DIRECTORY cmake/
  DESTINATION "share/${PROJECT_NAME}"
  FILES_MATCHING PATTERN "*.cmake"
)
