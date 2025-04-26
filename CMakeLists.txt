# Copyright here
#
# License here

cmake_minimum_required(VERSION 3.15...4.01)

message(STATUS "-------------------------------")
message(STATUS "CMake Version: ${CMAKE_VERSION}")
message(STATUS "-------------------------------")
message(STATUS "CMake SrcDir: ${CMAKE_SOURCE_DIR}")
message(STATUS "CMake BinDir: ${CMAKE_BINARY_DIR}")

if (POLICY CMP0048)
    cmake_policy(SET CMP0048 NEW) # Project Version
endif ()
if (POLICY CMP0091)
    cmake_policy(SET CMP0091 NEW) # MSVC Runtime Library
endif ()

##################
#    Settings    #
##################

# For clangd
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Disable in-source builds
set(CMAKE_DISABLE_SOURCE_CHANGES ON)
set(CMAKE_DISABLE_IN_SOURCE_BUILD ON)

# Set C/C++ Standard
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Other settings
set_property(GLOBAL PROPERTY USE_FOLDERS ON)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -DPR_DEBUG_BUILD")

#################
#    Project    #
#################

project(
    ProjectName
    VERSION 0.1.0
    DESCRIPTION "Description here"
    HOMEPAGE_URL "https://github.com/user/repository"
    LANGUAGES CXX
)

# Version
set(PR_VERSION_STRING "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}")
if (${CMAKE_BUILD_TYPE} STREQUAL Debug)
    set(PR_VERSION_STRING "${PR_VERSION_STRING}-debug")
endif ()

# Other project settings
if (MSVC)
    if (${CMAKE_BUILD_TYPE} STREQUAL Debug)
        set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreadedDebugDLL")
    else ()
        set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreadedDLL")
    endif ()
endif ()

########################
#    Subdirectories    #
########################

add_subdirectory(src)
