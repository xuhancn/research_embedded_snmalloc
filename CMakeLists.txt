cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

set(PROJ_NAME "embedded_snmalloc")
project (${PROJ_NAME})

set(PROJECT_ROOT_DIR ${PROJECT_SOURCE_DIR})
set(LIBRARY_OUTPUT_PATH ${PROJECT_ROOT_DIR}/lib)
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_ROOT_DIR}/bin)

set(SOURCES_FILES)
add_subdirectory(${PROJECT_ROOT_DIR}/src)
link_directories(${PROJECT_ROOT_DIR}/lib)

# built-in malloc
add_executable(${PROJ_NAME} ${SOURCES_FILES})

set(SNMALLOC_BUILD_TESTING OFF)
add_subdirectory(${PROJECT_ROOT_DIR}/third_party/snmalloc)

target_link_libraries(${PROJ_NAME} PRIVATE "snmallocshim-static")
add_dependencies(${PROJ_NAME} snmallocshim-static)