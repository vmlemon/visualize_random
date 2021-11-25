cmake_minimum_required(VERSION 2.6)
project(VISUALIZE_RANDOM_DISTRIBUTION)

set(EXECUTABLE_NAME "Visualize_random_distribution")

###############################################################
# Files to include
###############################################################

include_directories(${CMAKE_SOURCE_DIR}/include)

FILE(GLOB_RECURSE ALL_SOURCE_FILES 
	"${CMAKE_SOURCE_DIR}/source/*.h"
	"${CMAKE_SOURCE_DIR}/source/*.c"
)

SET( PROJ_SOURCES
	${ALL_SOURCE_FILES}
	)

###############################################################
# Compiler settings
###############################################################

# Initialize CXXFLAGS.
set(CMAKE_C_FLAGS			"-Wall -std=c99 -v -pedantic -Wextra")
set(CMAKE_C_FLAGS_DEBUG		"-O0 -g")
set(CMAKE_C_FLAGS_MINSIZEREL		"-Os -DNDEBUG")
set(CMAKE_C_FLAGS_RELEASE		"-O4 -DNDEBUG")
set(CMAKE_C_FLAGS_RELWITHDEBINFO	"-O2 -g")


IF(CMAKE_BUILD_TYPE MATCHES DEBUG)
    SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY "./Debug")
ELSEIF(CMAKE_BUILD_TYPE MATCHES RELEASE)
   SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY "./Release")
ELSE()
   SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY "./Output")
ENDIF()

find_library(METAL Metal)
if (NOT METAL)
    message(FATAL_ERROR "Metal not found")
endif()

find_library(COREFOUNDATION CoreFoundation)
if (NOT COREFOUNDATION)
    message(FATAL_ERROR "CoreFoundation not found")
endif()

find_library(COREAUDIO CoreAudio)
if (NOT COREAUDIO)
    message(FATAL_ERROR "CoreAudio not found")
endif()

find_library(COREGRAPHICSO CoreGraphics)
if (NOT COREGRAPHICSO)
    message(FATAL_ERROR "CoreGraphics not found")
endif()

find_library(AUDIO_TOOLBOX AudioToolbox)
if (NOT AUDIO_TOOLBOX)
    message(FATAL_ERROR "AudioToolbox not found")
endif()


find_library(AUDIO_UNIT AudioUnit)
if (NOT AUDIO_UNIT)
    message(FATAL_ERROR "AudioUnit not found")
endif()

find_library(GAMECONTROLLER GameController)
if (NOT GAMECONTROLLER)
    message(FATAL_ERROR "GameController not found")
endif()

find_library(FORCEFEEDBACK ForceFeedback)
if (NOT FORCEFEEDBACK)
    message(FATAL_ERROR "ForceFeedback not found")
endif()


find_library(COREHAPTICS CoreHaptics)
if (NOT COREHAPTICS)
    message(FATAL_ERROR "CoreHaptics not found")
endif()


find_library(COREVIDEO CoreVideo)
if (NOT COREVIDEO)
    message(FATAL_ERROR "CoreVideo not found")
endif()


find_library(CARBON Carbon)
if (NOT CARBON)
    message(FATAL_ERROR "Carbon not found")
endif()

find_library(COCOA Cocoa)
if (NOT COCOA)
    message(FATAL_ERROR "Cocoa not found")
endif()



find_library(ICONV iconv)
if (NOT ICONV)
    message(FATAL_ERROR "iconv not found")
endif()


find_library(IOKIT IOKit)
if (NOT IOKIT)
    message(FATAL_ERROR "IOKit not found")
endif()

#set(CMAKE_MODULE_PATH "./source/cmake" ${CMAKE_MODULE_PATH})
#find_package(SDLTTF REQUIRED)
#include_directories(${SDL2TTF_INCLUDE_DIR})

find_library(SDL2_LIBRARY NAME SDL2)
add_executable(${EXECUTABLE_NAME} ${PROJ_SOURCES})
target_link_libraries(${EXECUTABLE_NAME} ${LIB})
include_directories(${EXECUTABLE_NAME} ${SDL2_INCLUDE_DIRS})
target_link_libraries(${EXECUTABLE_NAME} ${SDL2_LIBRARIES})
target_link_libraries(${EXECUTABLE_NAME} "/opt/homebrew/lib/libSDL2.a")
target_link_libraries(${EXECUTABLE_NAME} ${AUDIO_UNIT})
target_link_libraries(${EXECUTABLE_NAME} ${METAL})
target_link_libraries(${EXECUTABLE_NAME} ${COREAUDIO})
target_link_libraries(${EXECUTABLE_NAME} ${COREFOUNDATION})
target_link_libraries(${EXECUTABLE_NAME} ${COREGRAPHICS})
target_link_libraries(${EXECUTABLE_NAME} ${AUDIO_TOOLBOX})
target_link_libraries(${EXECUTABLE_NAME} ${FORCEFEEDBACK})
target_link_libraries(${EXECUTABLE_NAME} ${GAMECONTROLLER})
target_link_libraries(${EXECUTABLE_NAME} ${IOKIT})
target_link_libraries(${EXECUTABLE_NAME} ${COCOA})
target_link_libraries(${EXECUTABLE_NAME} ${CARBON})
target_link_libraries(${EXECUTABLE_NAME} ${ICONV})
target_link_libraries(${EXECUTABLE_NAME} ${COREHAPTICS})
target_link_libraries(${EXECUTABLE_NAME} ${COREVIDEO})
#target_link_libraries(${EXECUTABLE_NAME} ${SDL2TTF_LIBRARY})
