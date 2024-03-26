cmake_minimum_required(VERSION 3.11)
include(FetchContent)

FetchContent_Declare(
  MCXA153_SDK
  GIT_REPOSITORY https://github.com/Microcontroller-CMake-Templates/MCXA153_SDK.git
  GIT_TAG        main
  SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/SDK
)

FetchContent_MakeAvailable(MCXA153_SDK)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_LIST_DIR}/SDK/toolchain_armgcc.cmake)

project(MCXA153_project C CXX ASM)

add_executable(MCXA153_BLINK.elf src/main.c ${STARTUP_SCRIPT_SOURCES})

