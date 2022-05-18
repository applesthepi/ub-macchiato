cmake_minimum_required(VERSION 3.15)
project(MACCHIATO)

file(GLOB_RECURSE MACCHIATO_SRC "include/*/*.cpp" "include/*.cpp")

add_library(MACCHIATO STATIC ${MACCHIATO_SRC})

if(MSVC)
	source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR}/include/MACCHIATO FILES ${MACCHIATO_SRC})
	target_compile_options(MACCHIATO PRIVATE "/MP")
endif()

find_package(Vulkan REQUIRED FATAL_ERROR)


add_dependencies(
	MACCHIATO imgui glfw glm freetype VulkanMemoryAllocator)

target_include_directories(
	MACCHIATO
	PUBLIC SYSTEM )

target_link_libraries(
	MACCHIATO
	PUBLIC imgui glfw glm freetype VulkanMemoryAllocator Vulkan::Vulkan
)

target_include_directories(
	MACCHIATO
	PUBLIC SYSTEM ${PROJECT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/include
	${UB_DEPENDENCIES_INCLUDE} ${CMAKE_INCLUDES})