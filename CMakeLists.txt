cmake_minimum_required(VERSION 3.0)

# Name of the project
project(SonicCD)

# Set up CMake modules path
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

## Build and link
# Add all the files needed to compile here
set(SONICCD_SOURCES
    ${CMAKE_SOURCE_DIR}/dependencies/all/theoraplay/theoraplay.c
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Animation.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Audio.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Collision.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Debug.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Drawing.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Ini.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Input.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Math.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Object.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Palette.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Player.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Reader.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/RetroEngine.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Scene.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Scene3D.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Script.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Sprite.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/String.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Text.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Userdata.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/Video.cpp
    ${CMAKE_SOURCE_DIR}/SonicCDDecomp/main.cpp
)

if (${CMAKE_SYSTEM} MATCHES "Darwin")
	set(SONICCD_SOURCES ${SONICCD_SOURCES} ${CMAKE_SOURCE_DIR}/dependencies/mac/cocoaHelpers.mm)
endif()

add_executable(${PROJECT_NAME} ${SONICCD_SOURCES})

# Find the libraries
find_package(SDL2 REQUIRED)

include_directories(
	dependencies/all/theoraplay
	${SDL2_INCLUDE_DIRS}
)

find_package(Vorbis)
find_package(VorbisFile)
find_package(Theora)

target_link_libraries(${PROJECT_NAME}
  SDL2
  vorbisfile
  vorbis
  theoradec
  ogg
  pthread
)

if (${CMAKE_SYSTEM} MATCHES "Darwin")
	add_framework
	find_library(FOUNDATION Foundation)
	include_directories(
		${FOUNDATION}
		${THEORA_INCLUDE_DIR}
		dependencies/mac
	)
	target_link_libraries(${PROJECT_NAME} ${FOUNDATION})
endif()
	