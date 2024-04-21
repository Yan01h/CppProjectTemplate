# Copyright here
#
# License here

#################
#    Sources    #
#################

set(${PROJECT_ABBREVIATION}_SOURCE_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp
)

######################
#    Thirdparties    #
######################

# Add any third-party libs here

####################
#    Executable    #
####################

add_executable(${CMAKE_PROJECT_NAME} ${${PROJECT_ABBREVIATION}_SOURCE_FILES})

set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

if(WIN32)
    set_target_properties(${CMAKE_PROJECT_NAME} PROPERTIES
        LINK_FLAGS_DEBUG "/SUBSYSTEM:CONSOLE"
        LINK_FLAGS_RELEASE "/SUBSYSTEM:WINDOWS /ENTRY:mainCRTStartup"
        LINK_FLAGS_MINSIZEREL "/SUBSYSTEM:WINDOWS /ENTRY:mainCRTStartup"
        LINK_FLAGS_RELWITHDEBINFO "/SUBSYSTEM:WINDOWS /ENTRY:mainCRTStartup"
    )
endif()

# Include paths
target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(${CMAKE_PROJECT_NAME} PRIVATE ${CMAKE_BINARY_DIR}/generated)

# Libraries
# target_link_libraries here

# Configuration
set(TEMP_VERSION_STRING "${${PROJECT_ABBREVIATION}_VERSION_STRING}") # Fix for configure_file not replacing outer variable values
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/cmake_config.h.in ${CMAKE_BINARY_DIR}/generated/cmake_config.h @ONLY)