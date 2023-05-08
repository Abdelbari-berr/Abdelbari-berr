# Nous voulons un cmake "récent" pour utiliser les dernières fonctionnalités
cmake_minimum_required(VERSION 3.0)

# Notre projet est étiqueté TrackMan
#
set(PROJECT_NAME TrackCalculatorAgent)
#
project(${PROJECT_NAME})
#

#
add_subdirectory(${PROJECT_SOURCE_DIR}/doc)
#
#ADD_SUBDIRECTORY( test )
#
#
#
set(LIBRARY_OUTPUT_PATH lib/${CMAKE_BUILD_TYPE})
set(LIBRARY_INSTALL_PATH ${CMAKE_SOURCE_DIR}/lib)
set(LIBRARY_SOURCE_PATH ${PROJECT_SOURCE_DIR}/lib)
#
set(PROJECT_INC inc ) 
set(PROJECT_LIBS lib) 
set(PROJECT_LLIBS m ) 
set(PROJECT_TEST test ) 
#
ADD_SUBDIRECTORY( ${PROJECT_TEST} )
#
# Trouver un package avec find_package
#
# find_package(GTK2 REQUIRED)
# find_package(PkgConfig)
# pkg_check_modules(GTK2 gtk+-2.0 REQUIRED)
# 
#------------------ OPTIONS ------------------------
#set(PROJECT_OPTIONS -g -Wall -O3 -DUNIX -DLOG_FLAGS)
set(PROJECT_OPTIONS  -Wall -O3 -DUNIX)
#
#------- set list files to compil to object files ------
#
file(
    GLOB_RECURSE
    source_file
    src/*
)

file(
    GLOB_RECURSE
    headers_file
    inc/*
)
#
# message("--------------------------------------------")
#execute_process(COMMAND bash -c "source ${CMAKE_SOURCE_DIR}/env_dev.sh")
#
# --- build project ${PRJECT_NAME} ----
foreach(TYPE_COMPIL static shared)
    if(${TYPE_COMPIL} MATCHES "static")
        add_library(${PROJECT_NAME}_${TYPE_COMPIL} STATIC ${source_file} ${headers_file} )
    else()
        add_library(${PROJECT_NAME}_${TYPE_COMPIL} SHARED ${source_file} ${headers_file} )
    endif()
    target_compile_options(${PROJECT_NAME}_${TYPE_COMPIL} PUBLIC ${PROJECT_OPTIONS})
    target_include_directories(${PROJECT_NAME}_${TYPE_COMPIL} PUBLIC ${PROJECT_INC})
    target_link_libraries(${PROJECT_NAME}_${TYPE_COMPIL}  ${PROJECT_LLIBS})
    #
    install (TARGETS ${PROJECT_NAME}_${TYPE_COMPIL} DESTINATION ${LIBRARY_SOURCE_PATH})
    install (TARGETS ${PROJECT_NAME}_${TYPE_COMPIL} DESTINATION ${LIBRARY_INSTALL_PATH})

endforeach(${TYPE_COMPIL})


