cmake_minimum_required(VERSION 3.22)

project(lshell)
add_library(lshell INTERFACE)

# Enable CMake support for ASM and C languages
enable_language(C ASM)

target_compile_definitions(lshell INTERFACE 
    SHELL_CFG_USER=<shell_config.h>
    $<$<CONFIG:Debug>:DEBUG>
)

target_include_directories(lshell INTERFACE
    ../../../Core/Inc
    src
    extensions/log
)

target_sources(lshell INTERFACE
    src/shell.c
    src/shell_companion.c
    src/shell_cmd_list.c
    src/shell_ext.c
    extensions/log/log.c
)

target_link_directories(lshell INTERFACE
)

target_link_libraries(lshell INTERFACE
)

# Validate that STM32CubeMX code is compatible with C standard
if(CMAKE_C_STANDARD LESS 11)
    message(ERROR "Generated code requires C11 or higher")
endif()


