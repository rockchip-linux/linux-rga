# License: Apache 2.0. See LICENSE file in root directory.
# Copyright(c) 2019 Intel Corporation. All Rights Reserved.
#  minimum required cmake version: 3.1.0
cmake_minimum_required(VERSION 3.1.0)

project(RgaDemo)

# Save the command line compile commands in the build output
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)
# View the makefile commands during build
#set(CMAKE_VERBOSE_MAKEFILE on)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-pointer-arith -Wno-int-to-pointer-cast")

set(ENV{PKG_CONFIG_PATH} "/opt/devkit/lib/pkgconfig")
find_package(PkgConfig REQUIRED)
pkg_check_modules(RGA REQUIRED librga)

include_directories(${RGA_INCLUDE_DIRS})
link_directories(${RGA_LIBRARY_DIRS})

add_subdirectory(rgaBlit)
add_subdirectory(rgaClip)
add_subdirectory(rgaCopy)
add_subdirectory(rgaRotation)
add_subdirectory(rgaSlt)
add_subdirectory(rgaUserspace)

file(GLOB DATA_FILES data/*.bin)
install(FILES ${DATA_FILES} DESTINATION ${CMAKE_INSTALL_BINDIR}/data)
