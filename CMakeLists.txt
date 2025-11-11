cmake_minimum_required(VERSION 3.16)
project(Qt5Gtk2 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt5 5.7.0 REQUIRED COMPONENTS Core Gui Widgets)

if(NOT Qt5Gui_PRIVATE_INCLUDE_DIRS)
    message(FATAL_ERROR "Qt5 private development headers not found.
Please install the 'qtbase5-private-dev' package (or the equivalent for your Linux distribution) and try again.")
endif()

find_package(GTK2 REQUIRED)
find_package(X11 REQUIRED)

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS   ON)

include_directories(
    ${GTK2_INCLUDE_DIRS}
    ${X11_INCLUDE_DIR}
)

add_subdirectory(src/qt5gtk2-qtplugin)
add_subdirectory(src/qt5gtk2-style)

include(GNUInstallDirs)
message(STATUS "Plugins will be installed to: ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}/qt5/plugins")

enable_testing()
add_subdirectory(tests)
