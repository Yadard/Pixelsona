cmake_minimum_required(VERSION 3.19)
project(Pixelsona VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR})
set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake-modules)
SET(CPACK_ERROR_ON_ABSOLUTE_INSTALL_DESTINATION OFF)

set(PIXELSONA_INCLUDE_DIR ${PROJECT_SOURCE_DIR}/include)

if(PACK)
    set(PIXELSONA_BIN_DIR bin)
else(PACK)
    set(PIXELSONA_BIN_DIR ${PROJECT_SOURCE_DIR}/build/bin)
endif(PACK)

include(CTest)
enable_testing()

include_directories(${PIXELSONA_INCLUDE_DIR})

file(COPY assets DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
add_subdirectory(src)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
