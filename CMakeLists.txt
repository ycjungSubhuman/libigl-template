cmake_minimum_required(VERSION 3.11)
project(example)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# libigl
option(LIBIGL_WITH_OPENGL            "Use OpenGL"         ON)
option(LIBIGL_WITH_OPENGL_GLFW       "Use GLFW"           ON)

find_package(LIBIGL REQUIRED QUIET)

file(GLOB MYLIB_SRC src/*.cpp)
add_library(mylib ${MYLIB_SRC})
target_include_directories(mylib PUBLIC include/)
target_link_libraries(mylib PUBLIC igl::core igl::opengl_glfw)

add_executable(demoapp app/demoapp)
target_link_libraries(demoapp PRIVATE mylib)
