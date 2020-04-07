cmake_minimum_required (VERSION 3.0)
project(CMakeBase)
set(CMAKE_CXX_STANDARD 11)

include_directories(src/engine/public)
file(GLOB_RECURSE SRC_CORE src/engine/private/*.cpp)


add_executable (${PROJECT_NAME} ${SRC_CORE} src/main.cpp)
find_package(SFML 2.5 COMPONENTS REQUIRED network audio graphics window system)
target_link_libraries(
	${PROJECT_NAME}
	opengl32 sfml-network sfml-audio sfml-graphics sfml-window sfml-system
)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${CMAKE_SOURCE_DIR}/res $<TARGET_FILE_DIR:${PROJECT_NAME}>/res)

add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
        ${SFML_DIR}/../../../bin $<TARGET_FILE_DIR:${PROJECT_NAME}>)