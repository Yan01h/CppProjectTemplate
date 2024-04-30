# Copyright here
#
# License here

#################
#    Sources    #
#################

set(PR_SOURCE_FILES
    ${CMAKE_CURRENT_SOURCE_DIR}/main.cpp
)

######################
#    Thirdparties    #
######################

# Add any third-party libs here

####################
#    Executable    #
####################

add_executable(Testsss ${PR_SOURCE_FILES})

set_target_properties(Testsss PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR})

if(WIN32)
    set_target_properties(Testsss PROPERTIES
        LINK_FLAGS_DEBUG "/SUBSYSTEM:CONSOLE"
        LINK_FLAGS_RELEASE "/SUBSYSTEM:WINDOWS /ENTRY:mainCRTStartup"
    )
endif()

# Include paths
target_include_directories(Testsss PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(Testsss PRIVATE ${CMAKE_BINARY_DIR}/generated)

# Libraries
# target_link_libraries here

# Configuration
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/cmake_config.h.in ${CMAKE_BINARY_DIR}/generated/cmake_config.h)