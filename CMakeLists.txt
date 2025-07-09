# == DO NOT EDIT THE FOLLOWING LINES for the Raspberry Pi Pico VS Code Extension to work ==
if(WIN32)
    set(USERHOME $ENV{USERPROFILE})
else()
    set(USERHOME $ENV{HOME})
endif()
set(sdkVersion 2.1.1)
set(toolchainVersion 14_2_Rel1)
set(picotoolVersion 2.1.1)
set(picoVscode ${USERHOME}/.pico-sdk/cmake/pico-vscode.cmake)
if (EXISTS ${picoVscode})
    include(${picoVscode})
endif()
# ====================================================================================
set(PICO_BOARD pico CACHE STRING "Board type")

# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# initalize pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
#set(PICO_SDK_PATH "/home/mark/pico-sdk")

# Pull in Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(pico-logic-analyser C CXX)

# Initialise the Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(pico-logic-analyser pico-logic-analyser.c )

pico_set_program_name(pico-logic-analyser "pico-logic-analyser")
pico_set_program_version(pico-logic-analyser "0.1a")

pico_enable_stdio_uart(pico-logic-analyser 0)
pico_enable_stdio_usb(pico-logic-analyser 1)

# Add the standard library to the build
target_link_libraries(pico-logic-analyser pico_stdlib hardware_pio hardware_dma)

pico_add_extra_outputs(pico-logic-analyser)
