cmake_minimum_required(VERSION 3.16)
set(CMAKE_CXX_STANDARD 17)

project(MyProject)

add_subdirectory(external)
find_package(Vulkan REQUIRED)

# 将源代码添加到此项目的可执行文件。

aux_source_directory(header HEAD)
aux_source_directory(src SRC)

add_executable(${PROJECT_NAME} ${HEAD} ${SRC} "main.cpp")

target_include_directories(${PROJECT_NAME} PUBLIC ./include)
target_include_directories(${PROJECT_NAME} PRIVATE ${Vulkan_INCLUDE_DIRS} external/glfw/include)
target_link_libraries(${PROJECT_NAME} Vulkan::Vulkan glm glfw stb)
target_compile_definitions(${PROJECT_NAME} PRIVATE GLFW_INCLUDE_NONE)
