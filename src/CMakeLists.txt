# Copyright here
#
# License here

#################
#    Sources    #
#################

set(
    PR_SOURCE_FILES
    main.cpp
)

######################
#    Thirdparties    #
######################

# Add any third-party libs here

####################
#    Executable    #
####################

add_executable(Executable ${PR_SOURCE_FILES})

if (WIN32)
    set_target_properties(
        Executable PROPERTIES
        LINK_FLAGS_DEBUG "/SUBSYSTEM:CONSOLE"
        LINK_FLAGS_RELEASE "/SUBSYSTEM:WINDOWS"
    )
endif ()

if (CMAKE_CXX_COMPILER_ID STREQUAL "MSVC")
    target_compile_options(Executable PRIVATE /W4 /WX)
else ()
    target_compile_options(Executable PRIVATE -Wall -Wextra -Wpedantic -Werror)
endif ()

# Include paths
target_include_directories(Executable PRIVATE ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_BINARY_DIR}/generated)

# Libraries
# target_link_libraries here

# Configuration
configure_file(cmake_config.h.in ${CMAKE_BINARY_DIR}/generated/cmake_config.h)