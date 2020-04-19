# set appropriate cmake version for gl
cmake_minimum_required(VERSION 3.10)
project(opengl-tutorial)

# ========================================================================== #
# language standard requirements
# ========================================================================== #

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


# ========================================================================== #
# OpenGL
# ========================================================================== #

if (POLICY CMP0072)
    set(OpenGL_GL_PREFERENCE LEGACY)
endif ()
find_package(OpenGL REQUIRED)
include_directories(${OpenGL_INCLUDE_DIRS})
link_directories(${OpenGL_LIBRARY_DIRS})
add_definitions(${OpenGL_DEFINITIONS})
if (NOT OPENGL_FOUND)
    message(ERROR " OPENGL not found!")
endif (NOT OPENGL_FOUND)


# ========================================================================== #
# GLFW
# ========================================================================== #

find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)
include_directories(${GLFW_INCLUDE_DIRS})


# ========================================================================== #
# X11 and pthread
# ========================================================================== #

find_package(X11 REQUIRED)
find_package(Threads)


# ========================================================================== #
# linker libraries and build executables
# ========================================================================== #

link_libraries(${OPENGL_LIBRARIES} ${GLFW_LIBRARIES} ${CMAKE_DL_LIBS} ${X11_LIBRARIES} ${CMAKE_THREAD_LIBS_INIT})
add_executable(tutorial_1 tutorial_1.cpp glad.c)
add_executable(tutorial_2 tutorial_2.cpp glad.c)
add_executable(tutorial_3 tutorial_3.cpp glad.c)