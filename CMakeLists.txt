cmake_minimum_required(VERSION 3.16)

project(vcpkgactiontestlib VERSION 0.1.0 LANGUAGES C)

include(GNUInstallDirs)
include(CMakePackageConfigHelpers)

add_library(vcpkgactiontestlib src/vcpkgactiontestlib.c)
add_library(vcpkgactiontestlib::vcpkgactiontestlib ALIAS vcpkgactiontestlib)

target_include_directories(
    vcpkgactiontestlib
    PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
        "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
)

install(
    TARGETS vcpkgactiontestlib
    EXPORT vcpkgactiontestlibTargets
    ARCHIVE DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
    INCLUDES DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}"
)

install(DIRECTORY include/ DESTINATION "${CMAKE_INSTALL_INCLUDEDIR}")

install(
    EXPORT vcpkgactiontestlibTargets
    NAMESPACE vcpkgactiontestlib::
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/vcpkgactiontestlib"
)

configure_package_config_file(
    cmake/vcpkgactiontestlibConfig.cmake.in
    "${CMAKE_CURRENT_BINARY_DIR}/vcpkgactiontestlibConfig.cmake"
    INSTALL_DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/vcpkgactiontestlib"
)

write_basic_package_version_file(
    "${CMAKE_CURRENT_BINARY_DIR}/vcpkgactiontestlibConfigVersion.cmake"
    VERSION "${PROJECT_VERSION}"
    COMPATIBILITY SameMajorVersion
)

install(
    FILES
        "${CMAKE_CURRENT_BINARY_DIR}/vcpkgactiontestlibConfig.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/vcpkgactiontestlibConfigVersion.cmake"
    DESTINATION "${CMAKE_INSTALL_LIBDIR}/cmake/vcpkgactiontestlib"
)
