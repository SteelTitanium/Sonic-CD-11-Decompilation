cmake_minimum_required(VERSION 3.0)

# Name of the project
project(SonicCD)

# Set up CMake modules path
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake/Modules/")

## Build and link
# Add all the files needed to compile here
add_executable(${PROJECT_NAME}
    ../dependencies/all/theoraplay/theoraplay.c
    ../SonicCDDecomp/Animation.cpp
    ../SonicCDDecomp/Audio.cpp
    ../SonicCDDecomp/Collision.cpp
    ../SonicCDDecomp/Debug.cpp
    ../SonicCDDecomp/Drawing.cpp
    ../SonicCDDecomp/Ini.cpp
    ../SonicCDDecomp/Input.cpp
    ../SonicCDDecomp/Math.cpp
    ../SonicCDDecomp/Object.cpp
    ../SonicCDDecomp/Palette.cpp
    ../SonicCDDecomp/Player.cpp
    ../SonicCDDecomp/Reader.cpp
    ../SonicCDDecomp/RetroEngine.cpp
    ../SonicCDDecomp/Scene.cpp
    ../SonicCDDecomp/Scene3D.cpp
    ../SonicCDDecomp/Script.cpp
    ../SonicCDDecomp/Sprite.cpp
    ../SonicCDDecomp/String.cpp
    ../SonicCDDecomp/Text.cpp
    ../SonicCDDecomp/Userdata.cpp
    ../SonicCDDecomp/Video.cpp
    ../SonicCDDecomp/main.cpp
)

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