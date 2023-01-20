cmake_minimum_required(VERSION 3.22)
project(try-xrpl)

find_package(SOCI REQUIRED)

add_subdirectory(external/rippled EXCLUDE_FROM_ALL)
target_link_libraries(xrpl_core PUBLIC soci::soci)

find_package(cpython 3.10.0 REQUIRED)

add_library(lib)
target_sources(lib PRIVATE src/lib.cpp)
target_link_libraries(lib PUBLIC
  xrpl_core
  cpython::python
)

add_executable(main)
target_sources(main PRIVATE src/main.cpp)
target_link_libraries(main PUBLIC lib)
