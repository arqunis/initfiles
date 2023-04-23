cmake_minimum_required(VERSION 3.16)

project(example
  LANGUAGES CXX
  VERSION 0.0.1
  DESCRIPTION "I am an example application built with CMake"
  HOMEPAGE_URL "https://example.com"
)

list(APPEND CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake)

include(GNUInstallDirs)

set(HEADERS
  include/example.hpp
)

add_library(example
  src/example.cpp
)

target_sources(example PRIVATE ${HEADERS})

target_compile_features(example PUBLIC cxx_std_17)

target_include_directories(example PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>)

add_library(example::example ALIAS example)

add_executable(program src/main.cpp)

target_compile_features(program PUBLIC cxx_std_17)

target_link_libraries(program PRIVATE example)

add_executable(example::program ALIAS program)

install(TARGETS example program
  EXPORT example-export
  RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
          COMPONENT ${CMAKE_PROJECT_NAME}_Runtime
  LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
          COMPONENT          ${CMAKE_PROJECT_NAME}_Runtime
          NAMELINK_COMPONENT ${CMAKE_PROJECT_NAME}_Development
  ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR}
          COMPONENT ${CMAKE_PROJECT_NAME}_Development
)

install(FILES ${HEADERS}
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
  COMPONENT ${CMAKE_PROJECT_NAME}_Development)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(exampleConfigVersion.cmake
  VERSION ${PROJECT_VERSION}
  COMPATIBILITY SameMajorVersion)

configure_package_config_file(
  ${PROJECT_SOURCE_DIR}/cmake/libraryConfig.cmake.in
  ${PROJECT_BINARY_DIR}/exampleConfig.cmake
  INSTALL_DESTINATION
  ${CMAKE_INSTALL_LIBDIR}/cmake/example
)

install(EXPORT example-export
  FILE exampleTargets.cmake
  NAMESPACE example::
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/example)

install(FILES
  ${PROJECT_BINARY_DIR}/exampleConfig.cmake
  ${PROJECT_BINARY_DIR}/exampleConfigVersion.cmake
  DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/example)

include(ClangFormat)
target_clangformat_setup(example)

enable_testing()
add_subdirectory(tests)
