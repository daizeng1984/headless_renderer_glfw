cmake_minimum_required(VERSION 3.2)

set(CMAKE_CXX_STANDARD 11)
project(headless_renderer)
SET(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} "-std=c++11")
SET(CMAKE_BUILD_TYPE Debug)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)
set(ASSIMP_BUILD_TESTS OFF CACHE BOOL "" FORCE)

add_subdirectory(external/glfw)
include_directories(external/glfw)
include_directories(external/glfw/deps)
include_directories(external/glfw/include)

# header only add_subdirectory(external/glm)
include_directories(external/glm)
include_directories(external/CLI11/include)

add_subdirectory(external/assimp)
include_directories(external/assimp)

set(GLAD "${GLFW_SOURCE_DIR}/deps/glad/glad.h"
         "${GLFW_SOURCE_DIR}/deps/glad.c")
set(GETOPT "${GLFW_SOURCE_DIR}/deps/getopt.h"
           "${GLFW_SOURCE_DIR}/deps/getopt.c")
set(TINYCTHREAD "${GLFW_SOURCE_DIR}/deps/tinycthread.h"
                "${GLFW_SOURCE_DIR}/deps/tinycthread.c")

set(SOURCE_FILES src/main.cpp)

add_executable(headless_renderer ${SOURCE_FILES} ${TINYCTHREAD} ${GETOPT} ${GLAD})

target_link_libraries(headless_renderer glfw ${GLFW_LIBRARIES} assimp)
