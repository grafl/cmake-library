cmake_minimum_required(VERSION 4.0)

project(cmake_library LANGUAGES CXX)

include(cmake/UpdateSubmodules.cmake)

add_library(cmake_library src/library.cpp)

set_target_properties(cmake_library
    PROPERTIES
        CMAKE_CXX_STANDARD 20
        CMAKE_CXX_STANDARD_REQUIRED ON
        CMAKE_CXX_EXTENSIONS OFF
)

include(GNUInstallDirs)

target_include_directories(cmake_library
    PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>"
        "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
)

install(TARGETS cmake_library
    EXPORT cmake_libraryTargets
        LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
        ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
        RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
        INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)

install(FILES src/library.h DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

install(EXPORT cmake_libraryTargets
    FILE cmake_libraryTargets.cmake
    NAMESPACE library::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/cmake_library
)

include(CMakePackageConfigHelpers)

configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_libraryConfig.cmake"
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/cmake_library
)

install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/cmake_libraryConfig.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/cmake_library
)

include(CTest)
message(STATUS "BUILD_TESTING: ${BUILD_TESTING}")
if(BUILD_TESTING)
    add_subdirectory(external)
    add_executable(cmake_library_test test/cmake_library_test.cpp)
    target_link_libraries(cmake_library_test PRIVATE GTest::gtest_main)
    include(GoogleTest)
    gtest_discover_tests(cmake_library_test)
endif(BUILD_TESTING)

