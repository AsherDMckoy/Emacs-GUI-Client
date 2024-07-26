cmake_minimum_required(VERSION 3.30.1)
project(
  emacsGUI
  VERSION 0.1.0
  LANGUAGES C CXX)
set(CMAKE_C_STANDARD 17)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS_RELEASE_INIT "-O3")
file(GLOB_RECURSE SOURCES "src/*.c*")
file(GLOB_RECURSE HEADERS "inlcude/*.h")

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

target_include_directories(${PROJECT_NAME} PRIVATE include)
# Find and link Vulkan
find_package(Vulkan REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE Vulkan::Vulkan)

# Find and link GLFW
find_package(glfw3 REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE glfw)

# Find and link OpenGL
find_package(OpenGL REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE OpenGL::GL)

# Find and link Freetype
find_package(Freetype REQUIRED)
target_link_libraries(${PROJECT_NAME} PRIVATE Freetype::Freetype)

# Set compiler warnings
if(MSVC)
  target_compile_options(${PROJECT_NAME} PRIVATE /W4)
else()
  target_compile_options(${PROJECT_NAME} PRIVATE -Wall -Wextra -Wpedantic)
endif()
