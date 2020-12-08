cmake_minimum_required(VERSION 2.8)

project(libmysqlasync C)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/")
find_package(MySQL)
IF (NOT ${MARIADB_FOUND})
  message(FATAL_ERROR "Not found any mysqlclient")
ENDIF()
find_package(Libuv)
IF (NOT ${LIBUV_FOUND})
  message(FATAL_ERROR "Not foud any libuv")
ENDIF()

include_directories("${MARIADB_INCLUDE_DIR}")
include_directories("${LIBUV_INCLUDE_DIR}")
include_directories("${PROJECT_SOURCE_DIR}/include")
link_directories(${CMAKE_SOURCE_DIR}/lib)

file(GLOB LIB_SOURCES "src/*.c")

set(GCC_COVERAGE_COMPILE_FLAGS "-std=gnu11")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${GCC_COVERAGE_COMPILE_FLAGS}")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${GCC_COVERAGE_COMPILE_FLAGS}")

add_library(mysqlasync STATIC ${LIB_SOURCES})

add_subdirectory(tests)

install(TARGETS mysqlasync DESTINATION lib)
install(DIRECTORY "${PROJECT_SOURCE_DIR}/include/" DESTINATION include/libmysqlasync)
