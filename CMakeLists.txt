cmake_minimum_required(VERSION 3.10)

project(xbouncing VERSION 0.0.0)

set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)

configure_file(
	src/config.h.in
	${CMAKE_BINARY_DIR}/config.h)

add_compile_options(-Wall -Wextra)

add_library(libxbouncing
	${CMAKE_BINARY_DIR}/config.h
	src/xbm.c
)

include(FindX11)

add_executable(xbouncing src/xbouncing.c)
add_executable(parse-xbm src/parse-xbm.c)
target_link_libraries(parse-xbm libxbouncing)
target_link_libraries(xbouncing libxbouncing ${X11_LIBRARIES} ${X11_Xrandr_LIB} m)
