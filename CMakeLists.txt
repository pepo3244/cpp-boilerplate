cmake_minimum_required(VERSION 3.0.0)

project(cpp-boilerplate VERSION 0.1.0 LANGUAGES CXX)

# enable fileter for Visual Studio
set_property(GLOBAL PROPERTY USE_FOLDERS ON)

file(GLOB_RECURSE SOURCE "Source/*.cpp" "Source/*.h")
add_executable(${PROJECT_NAME} WIN32 ${SOURCE} ".clang-format" ".editorconfig")

# filter setting for Visual Studio
source_group(TREE "${CMAKE_CURRENT_LIST_DIR}/Source" PREFIX "\\Source" FILES ${SOURCE})

# Visual StudioならCRTライブラリを静的リンクするように
target_compile_options(${PROJECT_NAME} PRIVATE
	$<$<CONFIG:>:/MT>
	$<$<CONFIG:Debug>:/MTd>
	$<$<CONFIG:Release>:/MT>
)

# 作業ディレクトリの設定
set_property(TARGET ${PROJECT_NAME} PROPERTY VS_DEBUGGER_WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR})

target_compile_definitions(${PROJECT_NAME} PRIVATE NOMINMAX)
