# Minimum required version of CMake
cmake_minimum_required(VERSION 3.10)

# Project name and a version number
project(Ensity-prj-1 VERSION 1.0)

# Specify the C standard
set(CMAKE_C_STANDARD 11)
set(CMAKE_C_STANDARD_REQUIRED True)

# Add an executable
add_executable(MyExecutable Main_program.c)

# Optionally, set compiler flags
# set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -Wall -Wextra")
