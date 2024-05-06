cmake_minimum_required(VERSION 3.10)
set(project_name hello_world)
project(${project_name} VERSION 1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
message(STATUS "Project source dir: ${PROJECT_SOURCE_DIR}")

if(MSVC)
    add_compile_options(/W4 /WX /Zi)
else()
    add_compile_options(-fdiagnostics-color=always -Wall -Wextra -Werror -std=c++17 -pedantic -g)
endif()

set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DDEBUG")

include_directories(${PROJECT_SOURCE_DIR}/include)

find_package(SDL2 REQUIRED)
find_package(Vulkan REQUIRED)

include_directories(${SDL2_INCLUDE_DIRS})
include_directories(${Vulkan_INCLUDE_DIRS})

file(GLOB SOURCES "src/*.cpp")

add_executable(${project_name} main.cpp ${SOURCES})

target_link_libraries(${PROJECT_NAME} ${SDL2_LIBRARIES} ${Vulkan_LIBRARIES})
