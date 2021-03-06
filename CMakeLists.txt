cmake_minimum_required(VERSION 3.1.0 FATAL_ERROR)
cmake_policy(SET CMP0048 NEW)

project(bidekkida VERSION 1.0.0 LANGUAGES C CXX)

find_package(Qt5 5.5.0 COMPONENTS Core REQUIRED)

# Auto generate moc files
set(CMAKE_AUTOMOC ON)

# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
set(CMAKE_INCLUDE_CURRENT_DIR ON)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
  set(CMAKE_INSTALL_PREFIX "/usr/local" CACHE PATH "Skaffari default install prefix" FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

set(CMAKE_INSTALL_BINDIR "${CMAKE_INSTALL_PREFIX}/bin" CACHE PATH "Directory to install skaffarictl")
set(CMAKE_INSTALL_DATADIR "${CMAKE_INSTALL_PREFIX}/share" CACHE PATH "Data install directory")
set(CMAKE_INSTALL_SYSCONFDIR "/etc" CACHE PATH "Directory to install configuration files")

# Enable C++11 features
set (CMAKE_CXX_STANDARD 11)

set (CMAKE_CXX_FLAGS_DEBUG "-Werror -Wall -Wcast-align -Wno-uninitialized -Wempty-body -Wformat-security -Wformat -Winit-self -fsanitize=address -ggdb")

set (QT_DEBUG "-DQT_NO_DEBUG -DQT_NO_DEBUG_OUTPUT")
if (${CMAKE_BUILD_TYPE} STREQUAL "Debug")
    set (QT_DEBUG "-DQT_DEBUG")
    message(STATUS "Enabling debug output")
endif(${CMAKE_BUILD_TYPE} STREQUAL "Debug")

add_definitions(${QT_DEBUG})

configure_file(src/config.h.in ${CMAKE_BINARY_DIR}/src/config.h)

include_directories(
    ${CMAKE_SOURCE_DIR}
    ${CMAKE_CURRENT_BINARY_DIR}
)

add_subdirectory(src)


