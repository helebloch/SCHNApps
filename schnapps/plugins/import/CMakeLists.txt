project(plugin_import
	LANGUAGES CXX
)

find_package(cgogn_core REQUIRED)
find_package(cgogn_io REQUIRED)
find_package(Qt5 COMPONENTS Widgets REQUIRED)
find_package(tinyxml2 REQUIRED)
find_package(lm6 REQUIRED)
find_package(ply REQUIRED)

set(HEADER_FILES
	dll.h
	import.h
)

set(SOURCE_FILES
	import.cpp
)

set(CMAKE_AUTOMOC ON)

add_library(${PROJECT_NAME} SHARED ${HEADER_FILES} ${SOURCE_FILES})

set_target_properties(${PROJECT_NAME} PROPERTIES DEBUG_POSTFIX "_d")
target_compile_definitions(${PROJECT_NAME} PRIVATE "-DSCHNAPPS_PLUGIN_IMPORT_DLL_EXPORT")

target_include_directories(${PROJECT_NAME} PUBLIC
	${tinyxml2_INCLUDE_DIRS}
	${lm6_INCLUDE_DIRS}
	${ply_INCLUDE_DIRS}
	$<BUILD_INTERFACE:${SCHNAPPS_SOURCE_DIR}>
	$<BUILD_INTERFACE:${CGOGN_SOURCE_DIR}>
	${CMAKE_CURRENT_SOURCE_DIR}
	${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(${PROJECT_NAME}
	schnapps_core
	${cgogn_core_LIBRARIES}
	${cgogn_io_LIBRARIES}
	${Qt5Widgets_LIBRARIES}
	${tinyxml2_LIBRARIES}
	${lm6_LIBRARIES}
	${ply_LIBRARIES}
)
