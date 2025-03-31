cmake_minimum_required(VERSION 4.0)

project(cmake_library LANGUAGES CXX)

add_library(${PROJECT_NAME} src/library.cpp)

set_target_properties(${PROJECT_NAME}
    PROPERTIES
        CMAKE_CXX_STANDARD 20
        CMAKE_CXX_STANDARD_REQUIRED ON
        CMAKE_CXX_EXTENSIONS OFF
)

include(GNUInstallDirs)

target_include_directories(${PROJECT_NAME}
    PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
        "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
)