cmake_minimum_required(VERSION 3.28)

set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(watools)

find_package(Qt6 REQUIRED 
  COMPONENTS 
  Gui Core Widgets)

set(CMAKE_AUTORCC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)

file(GLOB SOURCES 
	src/*.cpp
	src/*.hpp
	src/ui/**/*.ui
	src/ui/**/*.h
  src/resources/*.rc
	src/resources/*.qrc)

add_executable(${PROJECT_NAME} ${SOURCES})

if (MSVC)
  target_link_options(${PROJECT_NAME} PRIVATE
		"/SUBSYSTEM:WINDOWS")
endif()

target_link_libraries(${PROJECT_NAME} 
  PRIVATE 
    Qt6::Gui Qt6::Core Qt6::Widgets)
