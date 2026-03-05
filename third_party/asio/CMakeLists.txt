cmake_minimum_required(VERSION 3.8)

##
## PROJECT
## name and version
##
project(asio VERSION 1.0)

set(ASIO_BUILD_INTERFACE "${CMAKE_CURRENT_LIST_DIR}/include/")

add_library(${PROJECT_NAME} INTERFACE)
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

target_include_directories(
	${PROJECT_NAME} 
	INTERFACE
	$<BUILD_INTERFACE:${ASIO_BUILD_INTERFACE}>
	$<INSTALL_INTERFACE:include>
)

target_compile_features(${PROJECT_NAME} INTERFACE cxx_std_20)
