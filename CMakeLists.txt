# Copyright here
#
# License here

cmake_minimum_required(VERSION 3.15)

# Change these!
set(PROJECT_FULL_NAME "Project")
set(PROJECT_ABBREVIATION "PR")
set(PROJECT_CXX_STANDARD 20)
set(PROJECT_C_STANDARD 11)

message(STATUS "-------------------------------")
message(STATUS "CMake Version: ${CMAKE_VERSION}")
message(STATUS "-------------------------------")
message(STATUS "CMake SrcDir: ${CMAKE_SOURCE_DIR}")
message(STATUS "CMake BinDir: ${CMAKE_BINARY_DIR}")

cmake_policy(SET CMP0048 NEW) # Project Version
cmake_policy(SET CMP0091 NEW) # MSVC Runtime Library

##################
#    Settings    #
##################

# Disable in-source builds
set(CMAKE_DISABLE_SOURCE_CHANGES ON)
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)

# Set C/C++ Standard
set(CMAKE_CXX_STANDARD ${PROJECT_CXX_STANDARD})
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_C_STANDARD ${PROJECT_C_STANDARD})
set(CMAKE_C_STANDARD_REQUIRED ON)
set(CMAKE_C_EXTENSIONS OFF)

# Other settings
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -D${PROJECT_ABBREVIATION}_DEBUG_BUILD")

#################
#    Project    #
#################

project(
    ${PROJECT_FULL_NAME}
    VERSION 0.1.0
    DESCRIPTION "Description here"
    HOMEPAGE_URL "https://github.com/user/repository"
    LANGUAGES CXX
)

# Version
set(${PROJECT_ABBREVIATION}_VERSION_STRING "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}")
if(CMAKE_BUILD_TYPE STREQUAL Debug)
    set(${PROJECT_ABBREVIATION}_VERSION_STRING "${${PROJECT_ABBREVIATION}_VERSION_STRING}-debug")
endif()

# Other project settings
if(MSVC)
    add_compile_options(/MP) # For faster compile times
    if(CMAKE_BUILD_TYPE STREQUAL Debug)
        set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreadedDebugDLL")
    else()
        set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreadedDLL")
    endif()
endif()

########################
#    Subdirectories    #
########################

add_subdirectory(src)