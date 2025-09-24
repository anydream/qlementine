cmake_minimum_required(VERSION 3.21.0)

# Enable parallel build (not enabled by default on Windows).
set(CMAKE_BUILD_PARALLEL_LEVEL $ENV{NUMBER_OF_PROCESSORS})

# Set project information.
project("qlementine"
  LANGUAGES CXX
  VERSION 1.3.1.0
  DESCRIPTION "Modern QStyle for desktop Qt applications."
)
set(PROJECT_COPYRIGHT "© Olivier Cléro, MIT License.")


# Global flags.

# Using newest version of C++
set(CMAKE_CXX_STANDARD 23)

set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
if(NOT CMAKE_OSX_DEPLOYMENT_TARGET)
  set(CMAKE_OSX_DEPLOYMENT_TARGET "13.6")
endif()
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")

# Find Qt.
find_package(Qt6 REQUIRED COMPONENTS Core Widgets Svg)
qt_standard_project_setup(
  # REQUIRES 6.9.0
)

# The library.
add_subdirectory(lib)

# Example apps using the lib.
if(QLEMENTINE_SANDBOX)
  add_subdirectory(sandbox)
endif()

if(QLEMENTINE_SHOWCASE)
  add_subdirectory(showcase)
endif()
