cmake_minimum_required (VERSION 3.15)
project (twolame)

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/build)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR})


if (CROSS_COMPILE_ARM)
	execute_process(
		WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
		COMMAND ./autogen.sh --disable-maintainer-mode --host=arm)
	execute_process(
		WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
		COMMAND ./configure --host=arm)
else()
	execute_process(
		WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
		COMMAND ./autogen.sh --disable-maintainer-mode)
	execute_process(
		WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
		COMMAND ./configure)
endif()

include_directories("${PROJECT_SOURCE_DIR}/libtwolame")

add_subdirectory(libtwolame)
