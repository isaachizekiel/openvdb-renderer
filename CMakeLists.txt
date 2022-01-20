cmake_minimum_required(VERSION 3.16)

project(openvdb-renderer)

# general cmake settings
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# OpenGL
find_package(OpenGL REQUIRED)

# OpenVDB
set(OPENVDB_BUILD_AX ON)
set(USE_AX ON)
add_subdirectory(thirdparty/openvdb)

# GLFW
add_subdirectory(thirdparty/glfw)

# to be removed 
if(WIN32)
  find_package(GLEW REQUIRED)
endif()


# include directory
include_directories(${CMAKE_PROJECT_NAME} thirdparty/imgui)

# dear imgui
set(IMGUI_SRC
  thirdparty/imgui/imgui.cpp
  thirdparty/imgui/imgui_demo.cpp
  thirdparty/imgui/imgui_draw.cpp
  thirdparty/imgui/imgui_tables.cpp
  thirdparty/imgui/imgui_widgets.cpp
  thirdparty/imgui/backends/imgui_impl_glfw.cpp
  thirdparty/imgui/backends/imgui_impl_opengl3.cpp)

# src
set(SRC
  src/openvdb_view.cc  
  src/viewer/Camera.cc
  src/viewer/ClipBox.cc
  src/viewer/Font.cc
  src/viewer/RenderModules.cc
  src/viewer/Viewer.cc)

add_executable(${CMAKE_PROJECT_NAME} ${IMGUI_SRC} ${SRC})

#
target_link_libraries(${CMAKE_PROJECT_NAME}
  OpenGL::GL
  OpenGL::GLU
  glfw
  openvdb)

target_compile_definitions(${CMAKE_PROJECT_NAME} PRIVATE -DGL_GLEXT_PROTOTYPES=1)


