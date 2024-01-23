# Minimum required version of CMake
cmake_minimum_required(VERSION 3.10)

# Project name and version number
project(Ensity-prj-1 VERSION 1.0)

# Specify the C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)


# Add an executable
add_executable(main_program Main_program.c)

# Optionally, set compiler flags
# set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra")

# Ensure OBJCOPY is available
find_program(OBJCOPY NAMES objcopy)

if (OBJCOPY)
    # Create S19 file after build
    add_custom_command(TARGET main_program POST_BUILD
                       COMMAND ${OBJCOPY} --output-target=srec $<TARGET_FILE:main_program> ${CMAKE_CURRENT_BINARY_DIR}/main_program.s19)
else()
    message(WARNING "objcopy not found. S19 file will not be created.")
endif()

# Create a zip file with the executable and the S19 file
add_custom_target(zip ALL
                  COMMAND ${CMAKE_COMMAND} -E tar "cfv" "artifacts.zip" --format=zip
                  ${CMAKE_CURRENT_BINARY_DIR}/main_program
                  $<$<BOOL:${OBJCOPY}>:${CMAKE_CURRENT_BINARY_DIR}/main_program.s19>)
