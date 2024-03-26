# We need to specify the minimum version needed to run this script, as some features were added to CMake after 3.11.
# Such as FetchContent
cmake_minimum_required(VERSION 3.11)

# Add FetchContent CMake module to the project, to fetch the SDK from GitHub
include(FetchContent)

# Instruct FetchContent where to download the SDK from/to
FetchContent_Declare(
  MCXA153_SDK
  GIT_REPOSITORY https://github.com/Microcontroller-CMake-Templates/MCXA153_SDK.git
  GIT_TAG        main
  SOURCE_DIR ${CMAKE_CURRENT_LIST_DIR}/SDK
)

# Download the SDK, wait for the Download to finish
FetchContent_MakeAvailable(MCXA153_SDK)

# Set the environment symbols needed to compile for the MCXA153 using the CMake Toolchain file inside the MCXA153 SDK package
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_LIST_DIR}/SDK/toolchain_armgcc.cmake)

# Create the MCXA153_project 
# SPECIFY THAT IT USES C CXX AND ASM, ASM IS NEEDED FOR THE STARTUP SCRIPT!
project(MCXA153_project C CXX ASM)

# Add the executable, add the startup and system script to the source compilation list
# The ${STARTUP_SCRIPT_SOURCES} is defined in the CMake Toolchain file above 
# and contains a direct path to the sytem and startup source files!
add_executable(MCXA153_BLINK.elf src/main.c ${STARTUP_SCRIPT_SOURCES})

