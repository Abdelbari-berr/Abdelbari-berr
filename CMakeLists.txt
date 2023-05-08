# Nous voulons un cmake "récent" pour utiliser les dernières fonctionnalités
cmake_minimum_required(VERSION 3.0)
#
set(NAME_PROJECT TrackMan)
#
# Notre projet est étiqueté TrackMan
project(${NAME_PROJECT} VERSION 1.0.1)
#

configure_file(${CMAKE_CURRENT_SOURCE_DIR}/version.h.in ${CMAKE_CURRENT_SOURCE_DIR}/version.h)

#set(CMAKE_BUILD_TYPE Release)
set(CMAKE_BUILD_TYPE Debug)

# -+------------------- Config param de msg debug compil ------------------------#
#set(CMAKE_VERBOSE_MAKEFILE ON)
#set(CMAKE_RULE_MESSAGES ON)
#set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(CMAKE_LIBS_DIR libs)
set(CMAKE_CXX_STANDARD 14)

# list lib directories
#
file(
    GLOB
    lib_dependencies
    libs/*
)
#
# message ("les libs = ${lib_dependencies}") 
#
# INSERTION  des libs ds le projet
#
foreach(LIB_NAME ${lib_dependencies})
    add_subdirectory(${LIB_NAME})   
endforeach(${LIB_NAME}) 
#
# Add main program directory
#
add_subdirectory(TrackMan)   
#

#
#
#section CPack
#
SET(CPACK_PACKAGE_DESCRIPTION_SUMMARY "Tracker demo")
SET(CPACK_PACKAGE_VENDOR "Engymat")
SET(CPACK_PACKAGE_EXECUTABLES ${NAME_PROJECT})
include (CPack)



