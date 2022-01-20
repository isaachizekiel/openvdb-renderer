cmake_minimum_required(VERSION 3.16)

project(openvdb-renderer-gui)

# general cmake settings
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# OpenGL
find_package(OpenGL REQUIRED)

# GLFW
add_subdirectory(thirdparty/glfw)

# to be removed 
if(WIN32)
  find_package(GLEW REQUIRED)
endif()


# include directory
include_directories(${CMAKE_PROJECT_NAME}
  thirdparty/imgui/backends
  thirdparty/imgui)


# dear imgui
set(IMGUI_SRC
  thirdparty/imgui/imgui.cpp
  thirdparty/imgui/imgui_demo.cpp
  thirdparty/imgui/imgui_draw.cpp
  thirdparty/imgui/imgui_tables.cpp
  thirdparty/imgui/imgui_widgets.cpp
  thirdparty/imgui/backends/imgui_impl_glfw.cpp
  thirdparty/imgui/backends/imgui_impl_opengl3.cpp)

add_executable(${CMAKE_PROJECT_NAME} ${IMGUI_SRC} src/gui.cc)

#
target_link_libraries(${CMAKE_PROJECT_NAME}
  OpenGL::GL
  OpenGL::GLU
  glfw)


