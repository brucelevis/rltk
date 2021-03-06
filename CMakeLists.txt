cmake_minimum_required(VERSION 3.1)
project("rltk")

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/cmake_modules")
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED on)

find_package(ZLIB REQUIRED)
find_package(SFML 2 COMPONENTS system window graphics REQUIRED)
find_package(cereal REQUIRED)

add_library(rltk 	rltk/rltk.cpp
					rltk/texture_resources.cpp
					rltk/color_t.cpp
					rltk/virtual_terminal.cpp
					rltk/rng.cpp
					rltk/geometry.cpp
					rltk/input_handler.cpp
					rltk/font_manager.cpp
					rltk/gui.cpp
					rltk/layer_t.cpp
					rltk/gui_control_t.cpp
					rltk/virtual_terminal_sparse.cpp
					rltk/ecs.cpp
					rltk/xml.cpp
					rltk/perlin_noise.cpp
					rltk/rexspeeder.cpp
					rltk/scaling.cpp)
target_include_directories(rltk PUBLIC
		"$<BUILD_INTERFACE:${SFML_INCLUDE_DIR}>"
		"$<BUILD_INTERFACE:${CEREAL_INCLUDE_DIR}>"
		"$<BUILD_INTERFACE:${ZLIB_INCLUDE_DIRS}>"
		)
target_link_libraries(rltk PUBLIC ${ZLIB_LIBRARIES} ${SFML_LIBRARIES})
if(NOT MSVC) # Why was this here? I exempted the wierd linker flags
	target_compile_options(rltk PUBLIC -O3 -Wall -Wpedantic -march=native -mtune=native -g)
else()
	target_compile_options(rltk PUBLIC /W3 /EHsc)
endif()

install (TARGETS rltk
		ARCHIVE DESTINATION lib
		LIBRARY DESTINATION lib
		RUNTIME DESTINATION bin)

set(RLTK_HEADERS
		rltk/astar.hpp
		rltk/colors.hpp
		rltk/color_t.hpp
		rltk/ecs.hpp
		rltk/ecs_impl.hpp
		rltk/filesystem.hpp
		rltk/font_manager.hpp
		rltk/fsa.hpp
		rltk/geometry.hpp
		rltk/gui.hpp
		rltk/gui_control_t.hpp
		rltk/input_handler.hpp
		rltk/layer_t.hpp
		rltk/path_finding.hpp
		rltk/perlin_noise.hpp
		rltk/rexspeeder.hpp
		rltk/rltk.hpp
		rltk/rng.hpp
		rltk/scaling.hpp
		rltk/serialization_utils.hpp
		rltk/texture.hpp
		rltk/texture_resources.hpp
		rltk/vchar.hpp
		rltk/virtual_terminal.hpp
		rltk/virtual_terminal_sparse.hpp
		rltk/visibility.hpp
		rltk/xml.hpp)

install(FILES ${RLTK_HEADERS}
		DESTINATION "include/rltk"
		)

# Examples

# Add all of the example executables and their library dependency
add_executable(ex1 examples/ex1/main.cpp)
add_executable(ex2 examples/ex2/main.cpp)
add_executable(ex3 examples/ex3/main.cpp)
add_executable(ex4 examples/ex4/main.cpp)
add_executable(ex5 examples/ex5/main.cpp)
add_executable(ex6 examples/ex6/main.cpp)
add_executable(ex7 examples/ex7/main.cpp)
add_executable(ex8 examples/ex8/main.cpp)
add_executable(ex9 examples/ex9/main.cpp)
add_executable(ex10 examples/ex10/main.cpp)
add_executable(ex11 examples/ex11/main.cpp)
target_link_libraries(ex1 rltk)
target_link_libraries(ex2 rltk)
target_link_libraries(ex3 rltk)
target_link_libraries(ex4 rltk)
target_link_libraries(ex5 rltk)
target_link_libraries(ex6 rltk)
target_link_libraries(ex7 rltk)
target_link_libraries(ex8 rltk)
target_link_libraries(ex9 rltk)
target_link_libraries(ex10 rltk)
target_link_libraries(ex11 rltk)
