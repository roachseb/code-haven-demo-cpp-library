cmake_minimum_required(VERSION 3.20)
project(math-utils VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Library target
add_library(math-utils
    src/math_utils.cpp
)

target_include_directories(math-utils
    PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
)

# ── Install & CMake Package Export ────────────────────────────
# This makes the library consumable via find_package(math-utils)
include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

install(TARGETS math-utils
    EXPORT math-utils-targets
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
    INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
install(DIRECTORY include/ DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

# Generate and install CMake config files
install(EXPORT math-utils-targets
    FILE math-utils-targets.cmake
    NAMESPACE math-utils::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/math-utils
)

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/math-utils-config-version.cmake"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion
)

configure_package_config_file(
    "${CMAKE_CURRENT_SOURCE_DIR}/cmake/math-utils-config.cmake.in"
    "${CMAKE_CURRENT_BINARY_DIR}/math-utils-config.cmake"
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/math-utils
)

install(FILES
    "${CMAKE_CURRENT_BINARY_DIR}/math-utils-config.cmake"
    "${CMAKE_CURRENT_BINARY_DIR}/math-utils-config-version.cmake"
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/math-utils
)

# ── Testing ───────────────────────────────────────────────────
option(BUILD_TESTS "Build unit tests" ON)
if(BUILD_TESTS)
    enable_testing()
    add_subdirectory(tests)
endif()
